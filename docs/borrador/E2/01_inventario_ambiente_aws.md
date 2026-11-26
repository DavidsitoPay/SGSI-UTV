# E2 - Inventario del ambiente tecnológico implementado en AWS

## 1. Alcance y estado general

- Plataforma: AWS, cuenta identificada como "utv", región us-east-2. Plantillas en `infra/aws/` (orden de despliegue y desmontaje en `infra/aws/README.md`).
- Fecha de las verificaciones: 2026-11-25/26 (hora local y UTC según cada evidencia).
- Implementado y encendido (permanente): red (`utv-network`), identidad (`utv-identity`) y registro/monitoreo/respaldo (`utv-operations`), más la política de contraseñas de la cuenta (EV-E2-03, EV-E2-15).
- Implementado y verificado, actualmente apagado por diseño: la carga de trabajo (`utv-workload`: 1 EC2 y 1 RDS). Se desplegó, se verificó (EV-E2-05, EV-E2-06) y se eliminó; se recrea bajo demanda con el comando de `infra/aws/README.md` (EV-E2-15 muestra la ausencia de recursos residuales).
- Solo diseñado, no implementado: ver sección 5.

## 2. Inventario de recursos

Los identificadores provienen de los archivos de evidencia; los de la carga de trabajo corresponden a la corrida de verificación y cambian al recrearla.

| Recurso | ID / nombre | Stack | Componente E1 | Activo | Flujo | Estado | Evidencia |
|---|---|---|---|---|---|---|---|
| VPC y subredes (5) | utv-vpc; ver sección 3 | utv-network | Red virtual (E1 sec. 3.1) | A06 (base), A07 (contraparte cloud) | F-01..F-03 | Implementado permanente | EV-E2-04 |
| Grupos de seguridad (web, app, datos) | utv-network-WebSg, AppSg, DataSg | utv-network | Filtrado de tráfico | A07 | F-01..F-03 | Implementado permanente | EV-E2-04 |
| NACL por subred | web, app, datos, administración | utv-network | Filtrado de tráfico | A07 | F-01..F-03 | Implementado permanente (reglas observadas por subred en EV-E2-04; coinciden con `infra/aws/network.yaml`) | EV-E2-04 |
| Servidor web | utv-web-01 (i-042297dc7179ac8ac, corrida de verificación) | utv-workload | Servidores virtuales | A06 | F-01, F-05 | Implementado, verificado y apagado | EV-E2-05, EV-E2-15 |
| Base de datos PostgreSQL | utv-db-01 (db.t4g.micro, privada, cifrada, sin datos reales) | utv-workload | Subred de datos | A03, A09 (solo estructura, sin datos reales) | F-03 | Implementado, verificado y apagado | EV-E2-06, EV-E2-15 |
| Roles IAM con MFA (administración, auditoría) y roles de servicio (EC2, Backup) | AdminRole, AuditorRole, rol de instancia, rol de Backup | utv-identity | Identidades y MFA | A07 | F-05 | Implementado permanente (sin usuarios reales) | EV-E2-03 |
| Política de contraseñas de la cuenta | longitud mínima 14, expiración 90 días, no reutilización de 24 | (CLI, `password-policy.json`) | Identidades y MFA | A07 | F-05 | Implementado permanente | EV-E2-11 |
| CloudTrail | utv-trail | utv-operations | Registros | Transversal | F-06 | Implementado permanente | EV-E2-07 |
| VPC Flow Logs | fl-08cc808bcb54dff3f | utv-network | Registros | Transversal | F-06 | Implementado permanente | EV-E2-08 |
| Alarmas CloudWatch (9) | utv-ConsoleNoMfa, IamPolicyChange, NaclChange, RootUsage, SgChange, TrailChange, UnauthorizedApi, ec2-status, rds-freestorage | utv-operations / utv-workload | Monitoreo | Transversal | F-06 | Implementado (7 permanentes y 2 de la carga de trabajo; 8 en estado OK y 1 en INSUFFICIENT_DATA en la corrida de verificación) | EV-E2-09 |
| Presupuestos | utv-net-5usd, utv-gross-30usd | utv-operations | Gobierno de costos | - | - | Implementado permanente | EV-E2-10 |
| Bóveda y plan de respaldo | utv-backup-vault; plan utv-daily (diario, retención 7 días) | utv-operations | Almacenamiento y copias de seguridad | A08 | F-07 | Implementado permanente | EV-E2-12, EV-E2-13 |
| Puntos de recuperación | 2 imágenes de EC2 y 1 instantánea de RDS (ciclo de vida de 7 días) | utv-operations | Almacenamiento y copias de seguridad | A08 | F-07 | Implementado permanente (conservados tras el desmontaje) | EV-E2-13, EV-E2-15 |
| Capa de aplicación (A01, A02, A05) | subred utv-app sin servidor | utv-network | Subred de aplicaciones | A01, A02, A05 | F-02 | Diseñado; reglas implementadas, sin servidor | EV-E2-04 |
| Subred de administración | utv-admin sin servidor | utv-network | Subred de administración | A07 | F-05 | Diseñado; reglas implementadas, sin servidor | EV-E2-04 |
| VPN sitio a sitio | - | - | Puerta de enlace VPN | - | F-04 | Bloqueado por SCP | EV-E2-02 |
| GuardDuty, Security Hub, Inspector | - | - | Detección | Transversal | F-06 | Bloqueado por SCP | EV-E2-02 |

Activos de la Entrega 1 fuera de AWS: A04 (correo institucional), A10 (equipos administrativos), A11 (equipos de docentes) y A12 (biblioteca digital) no se despliegan en este ambiente.

## 3. Segmentación

| Subred | CIDR | AZ | ID | Uso | NACL / SG |
|---|---|---|---|---|---|
| utv-web | 10.30.2.0/24 | us-east-2a | subnet-05ce7ad0716440bac | Entrada web (servidor web) | NACL: entrada 443 y puertos efímeros, salida 443, efímeros y 8080 hacia la subred de aplicaciones; SG: entrada 443 |
| utv-app | 10.30.3.0/24 | us-east-2a | subnet-041995b4152b8ba76 | Aplicaciones (sin servidor) | NACL: entrada 8080 desde web, salida 5432 hacia datos; SG: entrada 8080 solo desde el SG web |
| utv-data-a | 10.30.4.0/24 | us-east-2a | subnet-0dbf6696d90a9d08a | Datos (RDS) | NACL: entrada 5432 desde la subred de aplicaciones; SG: entrada 5432 solo desde el SG de aplicaciones |
| utv-data-b | 10.30.6.0/24 | us-east-2b | subnet-0075155a71ab67e12 | Segunda subred de datos (requisito del grupo de subredes de RDS) | misma NACL que utv-data-a |
| utv-admin | 10.30.5.0/24 | us-east-2a | subnet-0441eff0ffa5bb821 | Administración y monitoreo (sin servidor) | NACL: tráfico interno de la VPC |

Sin NAT Gateway ni VPC endpoints (EV-E2-04, EV-E2-15). Sin SSH abierto a Internet: el acceso administrativo al servidor es por SSM (EV-E2-05). Reglas: `infra/aws/network.yaml`.

## 4. Flujos de la Entrega 1

| Flujo | Estado | Evidencia |
|---|---|---|
| F-01 Acceso a servicios web | Implementado: HTTPS respondió 200 en el servidor web durante la verificación | EV-E2-05 |
| F-02 Procesamiento académico | Reglas de red implementadas; sin servidor de aplicación, conectividad no verificada | EV-E2-04 |
| F-03 Acceso a datos | Reglas de red implementadas (5432 solo desde la capa de aplicaciones); base de datos privada y no pública; conectividad aplicación-base de datos no verificada | EV-E2-04, EV-E2-06 |
| F-04 Conectividad híbrida | Diseñado; la VPN está bloqueada por la SCP de la organización | EV-E2-02 |
| F-05 Administración | Roles IAM con MFA, política de contraseñas y acceso por SSM | EV-E2-05, EV-E2-11 |
| F-06 Monitoreo | CloudTrail, Flow Logs y alarmas | EV-E2-07, EV-E2-08, EV-E2-09 |
| F-07 Respaldo y recuperación | Plan de respaldo, respaldos bajo demanda y prueba de restauración | EV-E2-12, EV-E2-13, EV-E2-14 |
| F-08 Acceso de invitados | Red del campus; no aplica al ambiente AWS | - |

## 5. Diseñado frente a implementado

No implementado (diseño documentado, sin recursos desplegados):

- Túnel VPN sitio a sitio real; la SCP de la organización deniega la creación de VPN Gateway y Customer Gateway en us-east-2 (EV-E2-02).
- GuardDuty, Security Hub e Inspector: denegados por la SCP (EV-E2-02); se sustituyen parcialmente por alarmas de CloudTrail (EV-E2-09).
- Grupos IAM: denegados por la SCP (EV-E2-02); se usan solo roles.
- Servidores en las subredes de aplicaciones y administración (solo reglas de red).
- AWS Config, DLP, MDM, segundo EC2 y claves KMS propias (CMK); el cifrado usa claves administradas por AWS.
- Limitaciones conocidas: sin instantánea final de RDS al eliminar la carga de trabajo (base vacía); el grupo de seguridad por defecto de la VPC no se endureció.

## 6. Índice de evidencias

Carpeta: `docs/borrador/E2/evidencia/`. Cada archivo incluye en su primera línea el comando y la fecha.

| ID | Qué prueba |
|---|---|
| EV-E2-01 | Identidad de la cuenta y plan gratuito con créditos |
| EV-E2-02 | Denegaciones de la SCP (6) y acciones permitidas necesarias |
| EV-E2-03 | Estado de los stacks CloudFormation (con la carga de trabajo encendida) |
| EV-E2-04 | Subredes, grupos de seguridad, ausencia de NAT y de VPC endpoints |
| EV-E2-05 | Servidor web gestionado por SSM y HTTPS 200 |
| EV-E2-06 | RDS PostgreSQL privado y cifrado |
| EV-E2-07 | CloudTrail activo sin error de entrega |
| EV-E2-08 | Flow Logs activos |
| EV-E2-09 | Alarmas y su estado |
| EV-E2-10 | Presupuestos |
| EV-E2-11 | Política de contraseñas |
| EV-E2-12 | Plan y selección de respaldo |
| EV-E2-13 | Respaldos bajo demanda de EC2 y RDS completados |
| EV-E2-14 | Prueba de restauración (dos intentos) |
| EV-E2-15 | Desmontaje de la carga de trabajo y verificación de recursos residuales |

## 7. Prueba de restauración (EV-E2-14)

- Intento 1: FALLÓ. El respaldo se tomó 3 s después de escribir un archivo marcador sin sincronizar; la instancia restaurada no contenía el marcador. Causa no determinada.
- Intento 2: APROBADO. Marcador sincronizado, nuevo respaldo, restauración; los marcadores leídos antes y después coinciden.
- RTO medido (inicio de la restauración hasta lectura del marcador): 1 min 37 s, frente al RTO de 4 horas del BIA de la Gestión Académica (Entrega 1, Tabla 7).
- RPO: el plan es diario (24 h), mayor que el RPO de 1 hora del BIA para la Gestión Académica; la brecha queda abierta como insumo del tratamiento de riesgos. La base de datos tiene retención de respaldo automático de 1 día y esta prueba no restauró RDS.
- Se usó una segunda instancia EC2 temporal en cada intento; ambas se terminaron.

## 8. Vigencia y costo

- Cuenta en el plan gratuito con créditos (EV-E2-01): vence el 2027-05-26 o al agotarse los créditos; la evidencia debe capturarse antes.
- Presupuestos de alerta: utv-net-5usd (neto) y utv-gross-30usd (bruto) (EV-E2-10).
- Costo real: pendiente de consultar en la consola de Billing; este documento no lo estima.
- Suscripción SNS del tema utv-security-alerts: Confirmada (estado observado por el usuario en la consola el 2026-11-25).

## 9. Menciones a Azure en la Entrega 1 (para marcar, sin corregir)

`docs/entregado/01_entregable_1_diseno_inicial_sgsi.md` conserva referencias a Azure en las líneas 139, 141, 155, 170, 190, 227, 253, 268, 271, 273, 280, 297-301, 303, 305, 318, 332, 348, 352, 354, 358, 362, 370, 376, 401, 440 y 441. La plataforma vigente es AWS; este inventario traduce los componentes (VNet a VPC, NSG a grupos de seguridad y NACL, Entra ID a roles IAM, Azure Monitor a CloudTrail y CloudWatch, VPN Gateway a diseño bloqueado).
