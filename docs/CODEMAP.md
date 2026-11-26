# CODEMAP

Índice para ubicar documentos. Léelo primero; abre archivos solo en lo que señale. Rutas relativas al repo.

Punto de entrada para redactar lo pendiente: `docs/borrador/GUIA_DOCUMENTACION_PENDIENTE.md`.

Estado: proyecto solo de documentación (SGSI-UTV). Se actualiza dentro de cada tarea que cree, mueva o elimine archivos.

Abreviaturas: E1-E7 = entregables del enunciado del proyecto final (`docs/00_enunciado_proyecto_final.md`, secciones 9 y 13). "Entrega N" = entrega semanal del curso, con su propio enunciado.

## Dos numeraciones

Existen dos numeraciones distintas: las Entregas del curso y los códigos E# del proyecto final. El Entregable 3 mencionado en el enunciado de la Entrega 2 (crosswalk) no es el E3 del proyecto final; su enunciado aún no se recibió.

Mapeo propuesto por el orquestador; el usuario puede ajustarlo (por confirmar):

| Entrega del curso | Enunciado | Archivo entregado | Códigos E# que cubre | Equipo |
|---|---|---|---|---|
| Entrega 1 | `docs/01_enunciado_entrega_1.md` | `docs/entregado/01_entregable_1_diseno_inicial_sgsi.md` | E1 (escenario, alcance, arquitectura, diagrama); avance inicial de E2 (evidencia del ambiente); E4.1 (inventario, mín. 15 activos); E4.2 (BIA, mín. 5 procesos); parte de contexto y alcance de E3 | Arquitectura híbrida, Gestión de riesgos, Evidencia e implementación, Documentación y estilo |
| Entrega 2 | `docs/02_enunciado_entrega_2.md` | `docs/entregado/02_entregable_2_alcance_brechas_soa.md` | Análisis de brechas (cláusulas 4-10 y 93 controles del Anexo A) y SoA preliminar; alimenta E5.2 (matriz de controles) y parte de E3; entrega PDF (10-15 páginas más anexos) y hoja de cálculo xlsx con la SoA; base del crosswalk futuro y de la SoA final | Políticas y controles (con Gestión de riesgos como insumo y verificación de referencias ISO por Investigación y verificación de fuentes) |

Sin iniciar ni enunciado recibido: E4.3-E4.6, E5.1, E5.3, E6, E7, documento final (~40 páginas) y presentación.

## 1. Mapa de documentos

Plataforma: AWS (híbrida). Borradores en `docs/borrador/<entregable>/`; `docs/entregado/` solo lectura.

| Entregable | Archivo | Equipo | Estado |
|---|---|---|---|
| Entrega 1 (curso) | `docs/entregado/01_entregable_1_diseno_inicial_sgsi.md`; enunciado `docs/01_enunciado_entrega_1.md` | Arquitectura híbrida | Entrega 1 entregada; cobertura de E# por confirmar |
| Entrega 2 (curso) | `docs/entregado/02_entregable_2_alcance_brechas_soa.md`; enunciado `docs/02_enunciado_entrega_2.md` | Políticas y controles | Entrega 2 entregada; cobertura de E# por confirmar |
| E1 diseño de infraestructura | cubierto en `docs/entregado/01_entregable_1_diseno_inicial_sgsi.md` | Arquitectura híbrida | entregado vía Entrega 1; por confirmar |
| E2 entorno implementado | IaC `infra/aws/` (sección 3); inventario `docs/borrador/E2/01_inventario_ambiente_aws.md`; evidencias `docs/borrador/E2/evidencia/`; pruebas de controles `docs/borrador/E2/02_pruebas_controles.md`, pestañas de consola para exponer `docs/borrador/E2/04_pestanas_consola.md` y salidas `docs/borrador/E2/pruebas/` (incl. P05b); capturas de consola tomadas (C01-C10b, C12, C13; C11 no disponible) y su lista `docs/borrador/E2/capturas/LISTA_CAPTURAS.md`; README raíz `README.md` (resumen práctico: qué se hizo, cubre, no cubre); guion de exposición de 5 min `docs/borrador/E2/03_guion_exposicion.md` | Evidencia e implementación | red, identidad y registro desplegados en us-east-2 (cuenta utv); carga EC2+RDS bajo demanda (verificada, apagada); VPN, grupos IAM, GuardDuty, Security Hub e Inspector bloqueados por SCP (diseñados) |
| E3 modelo de gestión de seguridad | parcial en entregado/01 y entregado/02 | Políticas y controles | parcial (por confirmar) |
| E4 inventario, BIA, riesgos | E4.1 y E4.2 en `docs/entregado/01_entregable_1_diseno_inicial_sgsi.md` | Gestión de riesgos | E4.1-E4.2 entregados vía Entrega 1 (por confirmar); E4.3-E4.6 not started |
| E5 políticas y controles | E5.2 alimentado por `docs/entregado/02_entregable_2_alcance_brechas_soa.md` | Políticas y controles | parcial (por confirmar); E5.1 y E5.3 not started |
| E6 COBIT 2019 / ITIL 4 | _(sin archivo)_ | Gobierno y servicios de TI | not started |
| E7 BCP/DRP | _(sin archivo)_ | Continuidad y Data Center | not started |
| Documento final (~40 páginas) | _(sin archivo)_ | Documentación y estilo | not started |
| Guía de documentación pendiente | `docs/borrador/GUIA_DOCUMENTACION_PENDIENTE.md` (mapa de entregables E1-E7, discusión, documento final y presentación con estado; guía de trabajo por entregable; hallazgos; reglas y formato; checklist final). Autocontenida para quien redacte lo que falta | Documentación y estilo | redactada; sirve de punto de entrada para los compañeros |

## 2. Pendientes abiertos (por confirmar)

- El mapeo Entrega -> códigos E# de la sección "Dos numeraciones" es una propuesta por confirmar.
- entregado/02 referencia Tablas 4-6 que no existen en el archivo.
- entregado/02: inconsistencia de 31 vs 6 controles organizacionales.
- entregado/02: inconsistencia de 1,800 vs 1,950 personas.
- entregado/02 no incluye referencias NIST/CIS/Microsoft.
- La plataforma en `docs/entregado/` es Azure; se reescribirá para AWS.
- E2: el SCP de la organización deniega en us-east-2 VPN Gateway, Customer Gateway, iam:CreateGroup, GuardDuty, Security Hub e Inspector.
- E2: la cuenta está en el plan gratuito por créditos; vence 2027-05-26 o al agotar créditos; capturar evidencia antes.
- Dato de referencia: el Anexo A de ISO/IEC 27002:2022 tiene 93 controles repartidos en 37 organizacionales, 8 de personas, 14 físicos y 34 tecnológicos; los conteos "31 vs 6" de controles organizacionales en entregado/02 deben revisarse contra 37 (por confirmar).

## 3. Infraestructura AWS (IaC)

| Archivo | Stack | Contenido | Exports principales |
|---|---|---|---|
| `infra/aws/network.yaml` | utv-network | VPC, subredes, tablas de rutas, grupos de seguridad, NACL, Flow Logs | utv-network-VpcId, *SubnetId, WebSgId, AppSgId, DataSgId |
| `infra/aws/identity.yaml` | utv-identity | roles de administración y auditoría con MFA, roles de EC2 y Backup | utv-identity-Ec2InstanceProfileName, BackupRoleArn, AdminRoleArn, AuditorRoleArn |
| `infra/aws/operations.yaml` | utv-operations | CloudTrail, bucket de registros, alarmas, SNS, bóveda y plan de Backup, presupuestos | utv-operations-TrailName, TrailBucketName, BackupVaultName, AlarmTopicArn |
| `infra/aws/workload.yaml` | utv-workload | 1 EC2 t3.micro, 1 RDS PostgreSQL db.t4g.micro y sus 2 alarmas (bajo demanda) | - |
| `infra/aws/password-policy.json` | - | política de contraseñas de la cuenta (CLI) | - |
| `infra/aws/README.md` | - | despliegue, carga de trabajo arriba/abajo, desmontaje total | - |

Orden de despliegue y desmontaje: `infra/aws/README.md`. Seguimiento de la tarea E2: `odd/tasks/aws-e2-free-tier.md`.
