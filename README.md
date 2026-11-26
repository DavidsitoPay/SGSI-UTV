# SGSI-UTV

Sistema de Gestión de Seguridad de la Información de la Universidad Tecnológica del Valle (proyecto del curso). La arquitectura es híbrida: red del campus (on-premise) más una parte en AWS. Este repositorio contiene la documentación y la infraestructura como código de la parte AWS. Este README resume lo práctico: qué se construyó, cómo se opera, qué se probó y qué no se cubre.

## Qué se construyó en AWS

Región us-east-2, perfil `utv`. Todo es CloudFormation (`infra/aws/`) y usa solo capa gratuita o créditos.

| Pila | Contenido | Ciclo de vida |
|---|---|---|
| `utv-network` | VPC 10.30.0.0/16, subredes web, app, datos (2 AZ) y administración; grupos de seguridad, NACL por subred, VPC Flow Logs | Permanente |
| `utv-identity` | Roles de administración y auditoría que exigen MFA, roles de EC2 y de Backup, sin usuarios reales | Permanente |
| `utv-operations` | CloudTrail, bucket de registros, 7 alarmas de seguridad con correo (SNS), bóveda y plan de respaldo diario, 2 presupuestos | Permanente |
| `utv-workload` | 1 EC2 t3.micro (servidor web, HTTPS) y 1 RDS PostgreSQL privada y cifrada, sin datos reales | Bajo demanda |

Además se aplicó la política de contraseñas de la cuenta (longitud mínima 14, expiración 90 días, no reutilización de 24).

Puntos de diseño que se pueden comprobar en los archivos:

- Segmentación: solo el 443 llega al servidor web; la base de datos acepta el 5432 solo desde la capa de aplicaciones; no hay NAT ni SSH abierto. La administración es por Systems Manager.
- Identidad: los roles exigen `aws:MultiFactorAuthPresent`; una política de denegación bloquea acciones sin MFA.
- Registro y detección: CloudTrail, Flow Logs y alarmas de CloudWatch sobre llamadas no autorizadas, cambios de IAM, NACL, grupos de seguridad y CloudTrail, uso de root y consola sin MFA.
- Respaldo: AWS Backup, plan diario con retención de 7 días.

## Cómo se opera

El ambiente está apagado por defecto: las tres pilas permanentes no tienen IP pública, RDS, NAT ni endpoints, y la carga de trabajo solo se cobra mientras está arriba. Se necesita una sesión activa: `aws login --profile utv`.

- Levantar la carga de trabajo (EC2 y RDS):
  `aws cloudformation deploy --stack-name utv-workload --template-file infra/aws/workload.yaml --tags Project=SGSI-UTV --no-fail-on-empty-changeset --profile utv --region us-east-2`
- Apagarla:
  `aws cloudformation delete-stack --stack-name utv-workload --profile utv --region us-east-2` y esperar con `aws cloudformation wait stack-delete-complete`.
- Despliegue inicial y desmontaje total: `infra/aws/README.md`.

La RDS detenida se reinicia sola a los 7 días, por eso se elimina y se recrea en lugar de detenerla.

## Qué se probó

Hecho: pruebas P01-P10 (con P05b) del 26/11/2026, con la carga de trabajo levantada y desmontada después. Detalle en `docs/borrador/E2/02_pruebas_controles.md`; salidas sanitizadas en `docs/borrador/E2/pruebas/`.

| ID | Prueba | Resultado |
|---|---|---|
| P01 | HTTPS desde internet al servidor web | PASS (HTTP 200) |
| P02 | SSH (22) no accesible desde internet | PASS |
| P03 | Administración solo por SSM | PASS |
| P04 | Web no alcanza la base de datos (5432); base privada y cifrada | PASS |
| P05 | AssumeRole sin MFA denegado | PASS con limitación: el error no menciona MFA y el llamante no está en la política de confianza, así que no aísla la condición |
| P05b | Condición de MFA aislada con simulación de políticas | PASS (simulación); falta un AssumeRole real con dispositivo MFA |
| P06 | La SCP de la organización deniega GuardDuty | PASS |
| P07 | Las llamadas denegadas activan la alarma `utv-UnauthorizedApi` | PASS (OK a ALARM a las 16:15:19 UTC); el correo de aviso fue confirmado por el usuario |
| P08 | CloudTrail registra los eventos denegados | PASS |
| P09 | Flow Logs registran REJECT al puerto 22 | PASS con limitación: los orígenes son escáneres de internet, no el intento propio |
| P10 | Roles IAM con condición de MFA en la relación de confianza y política de contraseñas activa (lectura por CLI) | PASS; la política de contraseñas se evidencia por CLI porque la página de consola no está disponible en esta cuenta miembro de la organización |
| Restauración | Respaldo y restauración de la EC2 (EV-E2-14) | Intento 1 FAIL, intento 2 PASS |

Prueba de restauración: en el intento 1 el archivo marcador no apareció en la instancia restaurada (el respaldo se tomó 3 s después de una escritura sin sincronizar; la causa no se determinó). En el intento 2 se sincronizó el disco antes del respaldo y los marcadores coincidieron. RTO medido: 1 min 37 s, frente a los 4 h del BIA. La base de datos no se restauró en esta prueba.

## Qué cubre del enunciado de E2

- Entorno de nube con red segmentada, filtrado de tráfico y servidores virtuales.
- Identidades con MFA y política de contraseñas.
- Registro de auditoría, registro de red y monitoreo con alertas.
- Respaldo con prueba de restauración.
- Control de costos con presupuestos.
- Inventario de recursos enlazado a los activos y flujos de la Entrega 1, y evidencia por control (`docs/borrador/E2/evidencia/EV-E2-01..15`).

## Capturas de consola

Hecho: capturas C01-C13 (incluidas C03b, C05b, C08b, C10b, C11b, C11c) tomadas el 26/11/2026 y redactadas con cajas negras sobre información sensible; del ID de cuenta solo quedan los últimos 4 dígitos. Están en `docs/borrador/E2/capturas/` y se listan en `LISTA_CAPTURAS.md`. C11 no se pudo tomar y se sustituye por C11b, C11c y la salida de P10.

## Qué no cubre

- SIEM y EDR: GuardDuty, Security Hub e Inspector están bloqueados por una SCP de la organización (P06). Se sustituyen parcialmente por alarmas de CloudTrail y CloudWatch.
- VPN sitio a sitio: solo diseñada; la SCP deniega VPN Gateway y Customer Gateway.
- Grupos IAM: bloqueados por la SCP; se usan solo roles.
- DLP, MDM y AWS Config: no implementados.
- Las subredes de aplicaciones y de administración tienen reglas pero no servidores; la conectividad aplicación-base de datos no se verificó.
- Brecha de RPO: el BIA de Gestión Académica exige 1 h y el respaldo es diario (24 h). Queda abierta para el tratamiento de riesgos (E4).
- Un `AssumeRole` real con dispositivo MFA no se ha probado.

## Mapa del repositorio

| Ruta | Contenido |
|---|---|
| `infra/aws/` | Plantillas CloudFormation, política de contraseñas y README de operación |
| `docs/borrador/E2/` | Inventario, pruebas, evidencias, capturas y guion de exposición |
| `docs/entregado/` | Entregas 1 y 2. Todavía mencionan Azure y se reescribirán para AWS; solo lectura salvo aprobación |
| `docs/CODEMAP.md` | Índice de documentos y de la infraestructura |
| `odd/tasks/aws-e2-free-tier.md` | Seguimiento de la tarea E2 (especificaciones, tareas, registro) |
