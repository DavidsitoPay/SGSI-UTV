# Guion de exposición E2 - ambiente AWS (5 minutos)

La exposición total dura 10 minutos; esta parte es el bloque práctico de 5. No hay demostración en vivo: el ambiente se muestra apagado y cada bloque apoya lo que dice con capturas reales (`capturas/`, lista en `capturas/LISTA_CAPTURAS.md`) o con la salida de una prueba (`pruebas/`). Todo sale de `01_inventario_ambiente_aws.md`, `02_pruebas_controles.md` y `evidencia/EV-E2-*.md`.

Reparto: Expositor 1 = bloques 1 a 3; Expositor 2 = bloques 4 a 7 (cambiar nombres según el equipo).

## Antes de exponer

- [ ] Capturas abiertas en orden: C01, C02, C06, C03, C03b, C05, C05b, C11b, C11c, C08, C08b, C07, C13, C09, C10, C10b, C12.
- [ ] Versiones enmascaradas revisadas: cuenta (solo últimos 4 dígitos), IP, DNS y correos tapados.
- [ ] Abiertos en pestañas: diagrama de la Entrega 1, tabla de pruebas (`02_pruebas_controles.md`) y `pruebas/P05b.txt`, `pruebas/P06.txt`, `pruebas/P10_iam.txt`.
- [ ] Cronometrar un ensayo completo; si pasa de 5:00, recortar el bloque 4.

## Bloques

### 1. Alcance (0:00-0:35) - Expositor 1

- Mostrar: diagrama híbrido de la Entrega 1 y la tabla de pilas del README raíz.
- Decir: "Esta parte muestra lo que construimos en AWS. La arquitectura es híbrida: campus y nube. Dejamos cuatro pilas de CloudFormation: red, identidad, operaciones y una carga de trabajo que se levanta solo cuando hace falta. Hoy el ambiente está apagado, así que mostramos capturas reales tomadas durante las pruebas. Separamos siempre lo implementado de lo diseñado."

### 2. Arquitectura y segmentación (0:35-1:30) - Expositor 1

- Mostrar: C01 (VPC y subredes), C02 (grupo de seguridad web), C06 (NACL), C03/C03b (servidor sin llave ni IP de administración), C05/C05b (base privada y cifrada).
- Decir: "Una VPC con subredes separadas: web, aplicaciones, datos y administración. Al servidor web solo entra el 443; no hay SSH abierto y se administra por Systems Manager. La base PostgreSQL es privada, cifrada, y solo acepta el 5432 desde aplicaciones. Lo probamos: el SSH desde internet terminó por tiempo agotado y, desde el servidor web, el 5432 quedó bloqueado."
- Respaldo: salidas `pruebas/P02.txt` a `P04.txt`.

### 3. Identidad y MFA (1:30-2:20) - Expositor 1

- Mostrar: C11b (roles), C11c (relación de confianza con MFA), `pruebas/P10_iam.txt` y `pruebas/P05b.txt`.
- Decir: "Los roles de administración y auditoría exigen MFA en su relación de confianza, y una política deniega acciones sin MFA. La política de contraseñas pide 14 caracteres; la consola de la cuenta no mostró esa página, así que la comprobamos por línea de comandos. Asumir el rol sin MFA se denegó, y con simulación de políticas aislamos la condición: sin MFA se deniega, con MFA se permite. Un inicio de sesión real con dispositivo MFA no se probó."

### 4. Detección (2:20-3:30) - Expositor 2

- Mostrar: C08 y C08b (CloudTrail con AccessDenied), C07 (alarma de OK a ALARM), C13 (correo de aviso), C09 (Flow Logs).
- Decir: "Esta es la cadena de detección, ya probada. Hicimos llamadas denegadas por la organización o por IAM. CloudTrail las registró como AccessDenied. La alarma utv-UnauthorizedApi pasó de OK a ALARM a las 16:15 UTC y llegó el correo de aviso. Los Flow Logs registran rechazos al puerto 22, que son escáneres de internet."

### 5. Respaldo y restauración (3:30-4:15) - Expositor 2

- Mostrar: C10 y C10b (punto de recuperación y trabajos de restauración) y `evidencia/EV-E2-14.md`.
- Decir: "El respaldo es diario, con retención de 7 días. En la prueba de restauración el primer intento falló: el marcador no apareció, sin causa determinada; el respaldo se tomó sin sincronizar el disco. Sincronizamos y el segundo intento pasó, en 1 minuto 37 segundos, frente a 4 horas de RTO. La base de datos no se restauró. La brecha abierta es el RPO: 1 hora en el BIA contra 24 del respaldo."

### 6. Lo que no está implementado (4:15-4:50) - Expositor 2

- Mostrar: `pruebas/P06.txt` y tabla "Qué no cubre" del README raíz.
- Decir: "GuardDuty, Security Hub e Inspector están bloqueados por una política de la organización; la llamada real fue denegada. Lo sustituimos con alarmas de CloudTrail y CloudWatch. La VPN queda solo diseñada. DLP, MDM y AWS Config no se implementaron, y las subredes de aplicaciones y administración no tienen servidores."

### 7. Cierre (4:50-5:00) - Expositor 2

- Mostrar: C12 (presupuestos) y la tabla de resultados del README.
- Decir: "Diez pruebas de control en PASS, dos con limitación declarada, y una restauración que pasó en el segundo intento. Pasamos a la discusión."

## Palabras habladas

Los textos "Decir" de los bloques 1 a 7 suman unas 390 palabras (unos 3 minutos a ritmo normal). Si el ensayo pasa de 5:00, recortar los bloques 4 y 6.

## Preguntas probables

1. **¿Por qué no usaron GuardDuty o un SIEM?** Una SCP de la organización lo deniega en us-east-2; lo comprobamos con una llamada real (P06). Usamos alarmas de CloudTrail y CloudWatch como detección parcial.
2. **¿Cómo comprueban que el MFA funciona?** La confianza de los roles exige `aws:MultiFactorAuthPresent` (C11c, P10). P05b aísla la condición con simulación: sin MFA se deniega, con MFA se permite. Falta un AssumeRole real con dispositivo MFA.
3. **¿La detección funciona de extremo a extremo?** Sí: C08/C08b muestran los eventos denegados, C07 la transición a ALARM y C13 el correo recibido (P07, P08).
4. **¿Qué pasa con el RPO?** El BIA pide 1 h y el respaldo diario da 24 h. La brecha pasa al tratamiento de riesgos (E4).
5. **¿Por qué el ambiente está apagado?** La carga de trabajo (EC2 y RDS) se cobra solo mientras está arriba, y una RDS detenida se reinicia a los 7 días, por eso se elimina y se recrea con un comando. Las capturas C03 a C05b se tomaron con ella arriba.
6. **¿Qué es diseño y qué es implementado?** Sección 5 del inventario: VPN, detección administrada, grupos IAM, DLP, MDM y AWS Config solo se diseñaron; red, identidad, registro, alarmas, respaldo y la carga de trabajo se implementaron y probaron.
