# Pestañas de la consola AWS para la exposición E2

Región de todas las pestañas: us-east-2 (Ohio). El ambiente se muestra apagado, sin demostración en vivo. La carga de trabajo (EC2 y RDS) está eliminada: las consolas de EC2 y RDS mostrarán cero instancias. Para esos servicios se muestran solo las capturas C03/C03b/C04 (servidor web y Systems Manager) y C05/C05b (base de datos), no la consola.

## Pestañas, en el orden del guion

| # | Servicio (pestaña) | Ruta en la consola (us-east-2) | Qué se ve en vivo con todo apagado | Captura de respaldo | Qué decir |
|---|---|---|---|---|---|
| 1 | CloudFormation (bloque 1) | CloudFormation > Stacks | Pilas `utv-network`, `utv-identity`, `utv-operations`; `utv-workload` ausente | ninguna | "Cuatro pilas; la carga se levanta solo cuando hace falta." |
| 2 | VPC (bloque 2) | VPC > Your VPCs > utv (Resource map o Subnets) | VPC 10.30.0.0/16 y sus subredes | C01 `C01_vpc_subredes.png` | "Subredes separadas por función." |
| 3 | VPC - Security groups (bloque 2) | VPC > Security groups > SG web > Inbound rules | Solo el 443 de entrada, sin regla para el 22 | C02 `C02_sg_web.png` | "Al servidor web solo entra el 443." |
| 4 | VPC - Network ACLs (bloque 2) | VPC > Network ACLs | NACL por subred de la VPC utv | C06 `C06_nacls.png` | "Segunda capa de filtrado por subred." |
| 5 | EC2 (bloque 2) | solo capturas | Sin instancias (eliminadas) | C03 `C03_ec2_detalle.png`, C03b `C03b_ec2_seguridad.png`, C04 `C04_ssm_nodo.png` | "Sin llave ni IP de administración; se gestiona por Systems Manager." |
| 6 | RDS (bloque 2) | solo capturas | Sin bases de datos (eliminada) | C05 `C05_rds_conectividad.png`, C05b `C05b_rds_configuracion.png` | "Base privada y cifrada." |
| 7 | IAM - Roles (bloque 3) | IAM > Roles, filtrar por `Utv`; abrir `UtvAdminRole` > Trust relationships | Roles `Utv*` y la condición de MFA en la relación de confianza | C11b `C11b_iam_roles.png`, C11c `C11c_iam_trust.png` | "Los roles exigen MFA en la confianza." |
| 8 | CloudTrail (bloque 4) | CloudTrail > Event history, filtro Event name `CreateDetector` | Trail activo y eventos AccessDenied | C08 `C08_cloudtrail_denegados.png`, C08b `C08b_cloudtrail_detalle.png` | "Las llamadas denegadas quedan registradas." |
| 9 | CloudWatch - Alarms (bloque 4) | CloudWatch > Alarms > `utv-UnauthorizedApi` > History | Alarma y su transición OK a ALARM (26/11/2026 16:15 UTC) | C07 `C07_alarma_historial.png` | "La alarma pasó de OK a ALARM." |
| 10 | SNS (bloque 4) | solo captura (el correo del suscriptor es visible en vivo) | Tema `utv-security-alerts`; mostrar solo si se oculta la columna Endpoint | C13 `C13_correo_alarma_sns.png` | "Llegó el correo de aviso." |
| 11 | CloudWatch - Logs Insights (bloque 4) | CloudWatch > Logs Insights, grupo `/utv/vpc/flowlogs`, consulta con `action = "REJECT"` y `dstPort = 22` | Consulta ejecutable sobre registros ya almacenados; las IP de origen son visibles | C09 `C09_flowlogs_reject22.png` | "Rechazos al puerto 22 desde internet." |
| 12 | AWS Backup (bloque 5) | AWS Backup > Backup vaults > `utv-backup-vault` > Recovery points; luego Jobs > Restore jobs | Los puntos de recuperación caducan 7 días después de crearse: en una fecha posterior el vault puede estar vacío | C10 `C10_backup_restauracion.png`, C10b `C10b_backup_restore_jobs.png` | "Respaldo diario; restauración en 1 min 37 s." |
| 13 | Budgets (bloque 7) | Billing and Cost Management > Budgets | Los dos presupuestos (5 USD neto y 30 USD bruto) | C12 `C12_presupuestos.png` | "Costo controlado con alertas." |

Solo capturas: EC2 y RDS (filas 5 y 6). SNS (fila 10) también se prefiere en captura. Si la presentación es después de 7 días de la restauración, usar C10/C10b en lugar del vault.

## Privacidad antes de compartir pantalla

- [ ] La esquina superior derecha muestra el nombre completo del usuario y la cuenta.
- [ ] La barra de direcciones muestra el ID de cuenta.
- [ ] SNS muestra el correo del suscriptor.
- [ ] La lista de roles de IAM muestra el ID de la cuenta de administración de la organización.
- [ ] Logs Insights y CloudTrail pueden mostrar IP de origen y nombres de sesión.

Recomendación: presentar las capturas, ya enmascaradas, como material principal. Usar pestañas en vivo solo si al compartir se oculta la cabecera y la barra de direcciones, o ampliando (zoom) solo el área de contenido.

## Abrir antes, en este orden

1. CloudFormation, 2. VPC (Resource map), 3. Security groups, 4. Network ACLs, 5. IAM > Roles (con `UtvAdminRole` > Trust relationships), 6. CloudTrail > Event history, 7. CloudWatch > Alarms, 8. Logs Insights, 9. AWS Backup, 10. Budgets. Las capturas C03 a C05b, C10 y C13 se abren aparte, en el orden de `03_guion_exposicion.md`.
