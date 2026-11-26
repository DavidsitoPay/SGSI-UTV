# Lista de capturas de consola

Estado: tomadas el 2026-11-26 con el navegador Brave del usuario (sesion abierta y autenticada por el usuario, conexion CDP de depuracion; el agente no leyo credenciales, cookies ni almacenamiento). C11 no se pudo tomar como captura de la politica; se sustituye por C11b y C11c (roles IAM y relacion de confianza) y por la salida de CLI P10. Todas las capturas se revisaron y se tapo con cajas negras la informacion sensible; del ID de cuenta se conservan solo los ultimos 4 digitos. El entorno de carga se levanto para C03 a C05b y se desmonto despues.

Region de todas: us-east-2 (Ohio). Guardar como PNG en esta carpeta con el nombre indicado.

Enmascarar siempre en todas las capturas: ID de cuenta y nombre de usuario o rol en la cabecera de la consola, IP publicas y nombres DNS publicos, correos y el ID de la cuenta de administracion de la organizacion. No abrir ni mostrar valores de secretos.

| ID | Archivo | Ruta en la consola | Debe verse | Enmascarar | Estado |
|---|---|---|---|---|---|
| C01 | C01_vpc_subredes.png | VPC > Your VPCs > utv; pestana Resource map o Subnets | VPC 10.30.0.0/16 y subredes 10.30.2.0/24, 10.30.3.0/24, 10.30.4.0/24, 10.30.5.0/24 (y segunda AZ de datos) | cabecera | tomada: `capturas/C01_vpc_subredes.png` |
| C02 | C02_sg_web.png | VPC > Security groups > SG web > Inbound rules | solo 443 de entrada, sin regla para el 22 | cabecera, ID de cuenta en el ID del grupo si aparece | tomada: `capturas/C02_sg_web.png` |
| C03 | C03_ec2_detalle.png | EC2 > Instances > instancia web > Details y Security | estado Running, subred, SG, rol IAM, sin key pair | cabecera, IP publica, DNS publico | tomada: `capturas/C03_ec2_detalle.png (+ C03b_ec2_seguridad.png)` |
| C04 | C04_ssm_nodo.png | Systems Manager > Fleet Manager > Managed nodes | nodo de la instancia web en estado Online | cabecera, IP publica | tomada: `capturas/C04_ssm_nodo.png` |
| C05 | C05_rds_conectividad.png | RDS > Databases > utv-db-01 > Connectivity & security y Configuration | Publicly accessible: No; cifrado habilitado | cabecera, endpoint | tomada: `capturas/C05_rds_conectividad.png (+ C05b_rds_configuracion.png con cifrado)` |
| C06 | C06_nacls.png | VPC > Network ACLs | lista de NACL por subred de la VPC utv | cabecera | tomada: `capturas/C06_nacls.png` |
| C07 | C07_alarma_historial.png | CloudWatch > Alarms > utv-UnauthorizedApi > History | transicion OK a ALARM (26/11/2026 16:15:19 UTC) | cabecera, ARN con ID de cuenta | tomada: `capturas/C07_alarma_historial.png` |
| C08 | C08_cloudtrail_denegados.png | CloudTrail > Event history, filtro Event name AssumeRole y CreateDetector | eventos con error AccessDenied | cabecera, ID de cuenta y nombre de sesion en el usuario | tomada: `capturas/C08_cloudtrail_denegados.png (+ C08b_cloudtrail_detalle.png con AccessDenied; solo CreateDetector, no AssumeRole)` |
| C09 | C09_flowlogs_reject22.png | CloudWatch > Logs Insights, grupo /utv/vpc/flowlogs, consulta con action = "REJECT" y dstPort = 22 | registros REJECT al puerto 22 | cabecera, IP de origen | tomada: `capturas/C09_flowlogs_reject22.png` |
| C10 | C10_backup_restauracion.png | AWS Backup > Backup vaults > utv-backup-vault > Recovery points; luego Jobs > Restore jobs | punto de recuperacion y trabajo de restauracion completado | cabecera, ARN con ID de cuenta | tomada: `capturas/C10_backup_restauracion.png (+ C10b_backup_restore_jobs.png)` |
| C11 | C11_politica_contrasenas.png | IAM > Account settings > Password policy | parametros de la politica de contrasenas | cabecera | NO tomada (sustituida por `capturas/C11b_iam_roles.png` y `capturas/C11c_iam_trust.png`, y por `pruebas/P10_iam.txt`): IAM > Configuración de cuenta muestra "Característica no disponible" (requiere activar características avanzadas); la política se aplica por CLI (`infra/aws/password-policy.json`) |
| C12 | C12_presupuestos.png | Billing and Cost Management > Budgets | los dos presupuestos (5 USD neto y 30 USD bruto) | cabecera, ID de cuenta | tomada: `capturas/C12_presupuestos.png` |

Captura adicional (hecha como C13): si se usa el correo SNS de la alarma como captura, enmascarar el ID de cuenta, los ARN y el enlace de baja de suscripcion (contiene el correo).

**C13** (tomada): `capturas/C13_correo_alarma_sns.png`. Correo de alarma SNS de `utv-UnauthorizedApi` (OK -> ALARM, 26/11/2026 16:15:19 UTC), enmascarado según la regla de cuenta y correo; vinculada a P07.
