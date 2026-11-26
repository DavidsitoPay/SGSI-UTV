# Guía de documentación pendiente del SGSI-UTV

Esta guía es para quien redacte los entregables que faltan. No necesita haber leído ninguna conversación previa: indica qué pide el enunciado, qué existe ya en el repositorio, qué falta y qué reglas del curso hay que respetar. Las rutas son relativas a la raíz del repositorio. Las citas `00:123` apuntan a la línea 123 de `docs/00_enunciado_proyecto_final.md` (igual para `01:` y `02:` con los enunciados de las Entregas 1 y 2). Lo que el enunciado no aclara se marca "por confirmar con el docente".

## 1. El proyecto y su estado

El proyecto es el diseño e implementación de un SGSI para una universidad ficticia en Guatemala, la Universidad Tecnológica del Valle (UTV), con unos 1,800 estudiantes y 150 docentes y personal administrativo (`docs/entregado/01_entregable_1_diseno_inicial_sgsi.md`, sección 1.2). La arquitectura es híbrida: red del campus más una parte en nube pública. La plataforma elegida es **AWS** (el enunciado permite Azure, AWS o GCP, `00:57-63`). Los documentos ya entregados todavía dicen Azure y hay que reescribirlos a AWS.

En AWS ya existe un ambiente funcional, construido con CloudFormation en `infra/aws/` (región us-east-2, cuenta "utv"). Tres pilas permanentes están encendidas: red, identidad y registro/monitoreo/respaldo. Una cuarta, la carga de trabajo (1 servidor web EC2 y 1 base de datos RDS PostgreSQL sin datos reales), se desplegó, se probó y se eliminó para no gastar créditos; se recrea con un comando documentado en `infra/aws/README.md`. Cada prueba (P01 a P10), captura (C01 a C13) y evidencia (EV-E2-01 a EV-E2-15) está identificada y enlazada al elemento que prueba.

Dónde está cada cosa:

| Qué | Dónde |
|---|---|
| Enunciados | `docs/00_enunciado_proyecto_final.md`, `docs/01_enunciado_entrega_1.md`, `docs/02_enunciado_entrega_2.md` |
| Documentos ya entregados (solo lectura, dicen Azure) | `docs/entregado/01_entregable_1_diseno_inicial_sgsi.md`, `docs/entregado/02_entregable_2_alcance_brechas_soa.md` |
| Borradores del ambiente AWS (E2) | `docs/borrador/E2/`: inventario `01_inventario_ambiente_aws.md`, pruebas `02_pruebas_controles.md` y `pruebas/`, evidencias `evidencia/`, capturas `capturas/` y su lista, guion de exposición `03_guion_exposicion.md` |
| Infraestructura como código | `infra/aws/` |
| Resumen práctico | `README.md` en la raíz |
| Índice de archivos | `docs/CODEMAP.md` |

Reglas de trabajo del repositorio: los borradores nuevos van en `docs/borrador/<entregable>/`; `docs/entregado/` no se edita sin aprobación explícita. Dos numeraciones distintas conviven: las Entregas del curso (1, 2, ...) y los códigos E1 a E7 del proyecto final. El mapeo de una a otra está en `docs/CODEMAP.md` y es una propuesta, por confirmar.

## 2. Mapa de entregables

Estado: hecho, parcial o sin iniciar, según el contenido real de los archivos.

| Entregable | Qué pide el enunciado | Estado y ubicación | Qué falta |
|---|---|---|---|
| E1 Diseño de infraestructura (`00:111-152`) | Escenario, diagrama, componentes, flujos, segmentación, controles, redundancia, estrategia inicial de continuidad y justificación. Aprobación del diagrama por el docente (`00:150`) | Parcial. Sección 3 de `entregado/01`, pero en Azure; el diagrama es un marcador de imagen (línea 280) | Reescribir a AWS; exportar y redibujar el diagrama; confirmar que la aprobación del docente consta (se asumió dada con la Entrega 1) |
| E2 Ambiente implementado (`00:154-187`) | Descripción, evidencias, capturas, direccionamiento y segmentación, servicios, controles, pruebas, resultados; distinguir diseñado de implementado | Casi hecho, en borradores: `docs/borrador/E2/` (inventario, pruebas P01 a P10, 15 evidencias, 18 capturas) | Consolidar en un solo capítulo con el orden del enunciado; C11 no existe como captura; el costo real está pendiente de consultar en Billing |
| E3 Modelo de gestión (`00:189-208`) | Alcance, contexto, activos, procesos críticos, riesgos, controles, políticas, Zero Trust, incidentes, continuidad, gobierno y servicios | Parcial. Contexto y alcance en `entregado/01` (sec. 2) y `entregado/02` (sec. 2) | El modelo como tal (cómo se conectan las piezas, gestión de incidentes, roles). El enunciado no fija formato: por confirmar |
| E4.1 Inventario (`00:214-231`) | 12 campos mínimos por activo | Parcial. `entregado/01` sec. 5: 12 activos, 6 columnas | Ver sección 3.1 |
| E4.2 BIA (`00:233-248`) | Impactos por tipo, RTO, RPO, MTPD | Parcial. `entregado/01` sec. 6: 6 procesos, 5 columnas | Ver sección 3.1 |
| E4.3 Matriz de riesgos (`00:250-265`) | NIST SP 800-30: activo, amenaza, vulnerabilidad, probabilidad, impacto, riesgo inherente, controles existentes, riesgo residual | Sin iniciar | Todo |
| E4.4 OCTAVE (`00:267-280`) | Metodología, activos críticos, amenazas, escenarios, evaluación, resultados | Sin iniciar | Todo |
| E4.5 Matriz de calor (`00:282-288`) | Probabilidad × impacto como mínimo, con criterios de nivel definidos | Sin iniciar | Todo |
| E4.6 Plan de tratamiento (`00:290-310`) | Por riesgo: tratamiento, control, responsable, prioridad, plazo, estado, residual esperado | Sin iniciar | Todo |
| E5.1 Políticas (`00:312-371`) | Políticas mínimas en seis grupos: dominio e identidad, grupos, equipos, usuarios, nube, dispositivos móviles | Sin iniciar | Todo |
| E5.2 Matriz de controles (`00:373`) | Cada control ligado al riesgo que trata | Parcial. SoA preliminar en `entregado/02` (Entrega 2) | Corregir la SoA y ligarla a riesgos; ver 3.4 |
| E5.3 Buenas prácticas | Documento de buenas prácticas | Sin iniciar | Todo |
| E6 COBIT 2019 e ITIL 4 (`00:375-399`) | COBIT: gobierno, riesgos, cumplimiento, alineamiento, recursos, desempeño. ITIL: ocho prácticas listadas | Sin iniciar | Todo |
| E7 Continuidad y Data Center (`00:401-432`) | Estrategia, BCP, DRP, RTO, RPO, procedimientos, roles, pruebas; prácticas TIA-942 | Sin iniciar. Hay insumos reales: plan de respaldo y prueba de restauración (EV-E2-12 a 14) | Todo el documento |
| Discusión (`00:434-445`) | Seis preguntas (10.1 a 10.6) respondidas entre los integrantes, con fuentes confiables | Sin iniciar | Todo |
| Documento final (`00:447-485`) | Portada, tabla de contenido, 8 capítulos; el de resultados con 20 apartados mínimos. Unas 40 páginas (dato de `02:46`; `00` no fija extensión) | Sin iniciar | Ensamblar |
| Presentación y defensa (`00:614-648`) | 14 puntos mínimos; 15 a 25 minutos según el número de grupos, más una pregunta técnica | Parcial. Bloque de AWS en `docs/borrador/E2/03_guion_exposicion.md` (5 de 10 minutos) | El resto del guion y las diapositivas. El equipo maneja 10 minutos en total y el enunciado dice 15 a 25: por confirmar |

Cronograma del enunciado (`00:487-502`): semana 4, E3 y E4.1; semana 5, E4.2; semana 6, E4.3 y E4.4; semana 7, E4.5 y E4.6; semana 8, E5; semana 9, E6 y E7; semana 10, entrega final y defensa. Las fechas calendario no figuran en los archivos: por confirmar con el docente.

## 3. Guía por entregable pendiente

Normas que cada documento aplica al escenario (lista mínima del enunciado, `00:92-104`): ISO/IEC 27001, ISO/IEC 27002, ISO/IEC 27005, NIST SP 800-30, OCTAVE, NIST Cybersecurity Framework, Zero Trust Architecture, ISO 22301, COBIT 2019, ITIL 4 y TIA-942. Se citan por identificador y título, con análisis propio, sin copiar texto normativo (`02:24`). El enunciado no da la edición de ISO 22301 ni de TIA-942, no dice qué variante de OCTAVE usar y no cita un documento concreto para Zero Trust: por confirmar o verificar la fuente antes de citarla. `entregado/02` usa además Controles CIS v8.1, que el enunciado no pide; si se mantienen, hay que referenciarlos.

### 3.1 Completar E4.1 inventario y E4.2 BIA

Hallazgos sobre lo entregado (se comprueban contra `00:216-229`, `01:82-98` y `01:112-126`):

- El inventario tiene 12 activos (A01 a A12) y la Entrega 1 pide al menos 15, que incluyan información, sistemas, infraestructura, servicios, personas y proveedores. La tabla actual no tiene tipos "persona" ni "proveedor".
- Faltan columnas: descripción, custodio, ubicación, información procesada, confidencialidad, integridad, disponibilidad y dependencias. Hoy hay ID, activo, tipo, propietario, clasificación y criticidad.
- El BIA tiene 6 procesos (cumple el mínimo de 5) pero solo muestra proceso, impacto, nivel, RTO y RPO. Faltan responsable, impacto separado por operativo, financiero, reputacional, legal y académico, MTPD, activos que lo soportan, dependencias y prioridad de recuperación.
- El proceso Recursos Humanos no tiene un activo de sistema propio en A01 a A12 (solo A10, equipos administrativos). Decidir si falta un activo.

Insumos: la tabla de recursos de `docs/borrador/E2/01_inventario_ambiente_aws.md` (sección 2) mapea A01 a A12 a recursos AWS. A03 y A09 existen en AWS solo como estructura de base vacía; A01, A02 y A05 están diseñados con reglas de red pero sin servidor; A04, A10, A11 y A12 quedan fuera de AWS.

Vínculos exigidos (`01:144-146`): cada activo aparece en la arquitectura y cada proceso del BIA apunta a los activos que lo soportan. Propuesta, por validar: asignar IDs a los procesos (BIA-01 a BIA-06) para poder citarlos desde riesgos y plan de continuidad. Mantener el nombre y los IDs A01 a A12 sin renumerar, porque los borradores de E2 los citan.

### 3.2 E4.3 a E4.6 gestión de riesgos

Encadenamiento: activos (E4.1) y procesos (E4.2) alimentan la matriz de riesgos (E4.3); OCTAVE (E4.4) aporta una segunda vista con activos críticos y escenarios; la matriz de calor (E4.5) clasifica los riesgos de E4.3; el plan (E4.6) asigna tratamiento y control a cada riesgo.

- E4.3: usar NIST SP 800-30 para la evaluación y ISO/IEC 27005 como guía de proceso. Una fila por combinación activo-amenaza-vulnerabilidad, con las ocho columnas de `00:254-263`. Definir las escalas de probabilidad e impacto en el propio documento.
- E4.4: explicar qué variante de OCTAVE se usa y por qué se ajusta a una universidad de ese tamaño; después activos críticos, amenazas, escenarios, evaluación y resultados. Debe ser coherente con E4.3, no repetirla.
- E4.5: definir criterios de nivel (por ejemplo, rangos de la puntuación) antes de dibujar la matriz. Cada riesgo de E4.3 debe aparecer en una celda.
- E4.6: cada riesgo con mitigar, evitar, transferir o aceptar, más control, responsable (rol, no nombre), prioridad, plazo, estado y riesgo residual esperado. El control debe ser uno de la matriz E5.2.

Semillas de riesgo con evidencia real (propuestas, a evaluar y no a copiar sin análisis): brecha de RPO frente al respaldo diario; ausencia de detección gestionada por bloqueo de la organización; acceso administrativo sin MFA (probado en P05/P05b); exposición de la base de datos (probado en P04); vencimiento de créditos de la cuenta. Ver sección 4.

### 3.3 E3 modelo de gestión y E5.1 y E5.3 políticas y buenas prácticas

- E3: reutilizar contexto, alcance, partes interesadas y estándares de `entregado/01` y `entregado/02` (sec. 2). Añadir el modelo propiamente dicho: cómo se relacionan alcance, riesgos, controles, políticas, Zero Trust, incidentes, continuidad, gobierno y servicios. Un diagrama de relaciones ayuda y sirve de mapa para el resto del documento final.
- E5.1: una política por tema mínimo del enunciado (`00:316-365`). Para cada una: propósito, alcance, reglas, responsables por rol, relación con el riesgo y el control que respalda. Las políticas de dispositivos móviles (MDM, DLP, BYOD) son diseño: no hay MDM ni DLP implementados (se declararon fuera de alcance del ambiente AWS).
- Conflicto de alcance por resolver: `entregado/01` (sec. 2.4) deja fuera los dispositivos personales no administrados, pero el enunciado exige soporte para dispositivos móviles (`00:53`) y políticas BYOD (`00:364`). Decidir cómo se redacta el alcance: por confirmar con el docente.
- E5.3: buenas prácticas aplicadas al escenario, no genéricas. Las prácticas de nube se pueden respaldar con lo ya implementado: roles con MFA, política de contraseñas (longitud mínima 14, expiración 90 días, no reutilización de 24), segmentación, ausencia de SSH abierto, cifrado, respaldo.

### 3.4 E5.2 matriz de controles y SoA

La Entrega 2 (`02:26-40`) pide la SoA sobre los 93 controles del Anexo A de ISO/IEC 27001:2022 con siete columnas (control, tema, aplica, justificación, estado, responsable por rol, referencia). La E5.2 del proyecto final añade la relación de cada control con el riesgo que trata (`00:373`). La SoA debe ser coherente con alcance, riesgo y brechas (`02:53`).

Trabajo: partir de la SoA entregada, corregir las inconsistencias de la sección 4, añadir la columna de riesgo y una columna de evidencia. Los controles de ISO/IEC 27002:2022 tienen cuatro temas (organizacional 37, personas 8, físico 14, tecnológico 34; ver `docs/CODEMAP.md`, sección 2).

Controles con evidencia propia en AWS que pueden pasar a "implementado" con la salvedad que corresponda (verificar los títulos contra la norma antes de citarlos):

| Control (ISO/IEC 27002:2022) | Evidencia en el repositorio |
|---|---|
| 5.15 Control de acceso, 8.5 Autenticación segura | Roles con MFA en la relación de confianza (P05, P05b, P10; capturas C11b y C11c; EV-E2-03) |
| 8.2 Derechos de acceso privilegiados | Roles de administración y auditoría separados; sin grupos IAM por bloqueo de la organización (EV-E2-02) |
| 8.20 Seguridad de redes, 8.22 Segregación de redes | Subredes, grupos de seguridad y NACL (P02, P04; C01, C02, C06; EV-E2-04) |
| 8.15 Registro, 8.16 Actividades de monitoreo | CloudTrail, Flow Logs y alarmas (P07 a P09; C07 a C09; EV-E2-07 a 09) |
| 8.13 Respaldo de la información | Plan diario y prueba de restauración (EV-E2-12 a 14; C10) |
| 8.24 Uso de criptografía | Base de datos cifrada con clave administrada por AWS (EV-E2-06; C05b) |

### 3.5 E6 COBIT 2019 e ITIL 4

Aplicar al escenario, no describir los marcos. Para COBIT, usar los seis aspectos de `00:380-386` y ligar cada uno a decisiones reales de UTV (quién decide, qué se mide, qué riesgos gobierna). Para ITIL, las ocho prácticas de `00:389-397`; varias ya tienen insumos: gestión de cambios (la infraestructura como código en `infra/aws/` deja trazabilidad de cada cambio), gestión de activos y de configuración (inventario E4.1 e inventario de recursos de E2), gestión de continuidad (E7). Mostrar cómo se complementan ambos marcos responde también la pregunta 10.6.

### 3.6 E7 continuidad y Data Center

- Continuidad (`00:403-414`): estrategia, BCP, DRP, RTO y RPO por proceso tomados del BIA, procedimientos de recuperación, roles y pruebas. Insumo real: la prueba de restauración de EV-E2-14 (ver sección 4).
- Data Center (`00:416-430`): buenas prácticas TIA-942 sobre energía, UPS, generadores, climatización, cableado, redundancia, seguridad física, control de acceso, protección contra incendios, monitoreo y resiliencia. Ninguna está implementada ni medida en el repositorio: es redacción de diseño para el centro de datos del campus. En AWS la infraestructura física es del proveedor; el documento debe decir qué parte se hereda y qué parte queda en el campus.
- Coherencia obligada: los RTO y RPO de E7 son los del BIA (E4.2).

### 3.7 Discusión (sección 10 del enunciado)

Seis preguntas: Zero Trust en nube pública frente a híbrida, MDM y DLP, cumplimiento normativo local e internacional, aporte de SIEM, EDR y XDR, mejora continua tras una certificación ISO/IEC 27001, y complementariedad de COBIT e ITIL (`00:436-443`). Las respuestas se sustentan en fuentes académicas, técnicas o normativas (`00:445`). El enunciado dice "discusión académica entre los maestrandos del grupo" sin precisar el formato (diálogo, posiciones individuales o respuesta única): por confirmar. Puntos del ambiente construido que sirven de ejemplo honesto: en 10.1, la VPN híbrida quedó bloqueada y por eso solo está diseñada; en 10.4, GuardDuty, Security Hub e Inspector están denegados por la organización y se sustituyen por alarmas de CloudTrail y CloudWatch, sin SIEM, EDR ni XDR.

### 3.8 Documento final y presentación

- Estructura fija (`00:449-460`): portada, tabla de contenido, introducción, marco teórico, metodología, resultados, discusión, conclusiones, referencias y anexos. El capítulo de resultados incluye 20 apartados mínimos (`00:464-483`). El enunciado prohíbe definiciones teóricas sin aplicación (`00:107`) y a la vez pide marco teórico: se resuelve escribiendo el marco con la aplicación al escenario. Por confirmar con el docente.
- El contenido de las Entregas 1 y 2 debe poder integrarse sin reescribirlo (`02:46`) y conservarse y mejorarse (`01:151`).
- Anexos: SoA completa, matriz de brechas, matrices de riesgo, evidencias numeradas, salidas de pruebas.
- Presentación: 14 puntos mínimos (`00:620-635`). El bloque práctico de E2 ya tiene guion; falta el resto. Cada integrante debe poder responder sobre todo el proyecto (`00:648`).

## 4. Hallazgos ya identificados

1. Brecha de RPO. El BIA de Gestión Académica exige RPO de 1 hora, y el plan de respaldo de AWS es diario (24 horas). Los seis RPO del BIA (de 1 a 8 horas) son menores que 24 horas. La base de datos RDS tiene retención de respaldo automático de 1 día. Insumo directo para E4.3 y E4.6 (riesgo y tratamiento: aumentar la frecuencia, aceptar con justificación o revisar el RPO del BIA) y para E7. Fuente: `docs/borrador/E2/01_inventario_ambiente_aws.md`, sección 7.
2. Bloqueos de la organización (SCP). La organización a la que pertenece la cuenta deniega en us-east-2 la creación de VPN Gateway, Customer Gateway, grupos IAM, GuardDuty, Security Hub e Inspector (6 denegaciones, EV-E2-02, P06 PASS). Se documentan de dos maneras. Como control preventivo a nivel de organización: lo que la organización prohíbe, la cuenta no lo puede crear, y eso queda probado. Como componentes "diseñados, no implementados": la VPN sitio a sitio (flujo F-04) y los servicios de detección. Como sustituto parcial se usan alarmas sobre CloudTrail (P07, P08).
3. Prueba de restauración (EV-E2-14). El intento 1 falló (la instancia restaurada no tenía el marcador; causa no determinada) y el intento 2 pasó. RTO medido: 1 min 37 s, frente al RTO de 4 horas del BIA de Gestión Académica. Limitación: se restauró un servidor EC2, no la base de datos RDS. Se informan los dos intentos; no se omite el fallido.
4. Azure en lo entregado. `docs/entregado/` dice Azure en todo el diseño (lista de líneas en el inventario E2, sección 9). Al reescribir: VNet pasa a VPC, NSG a grupos de seguridad y NACL, Entra ID a roles IAM, Azure Monitor a CloudTrail y CloudWatch, VPN Gateway a diseño bloqueado. La sección 4 de `entregado/01` aún describe el ambiente como propuesta y debe sustituirse por la evidencia de E2. Se añadió una segunda subred de datos (10.30.6.0/24, otra zona) que el diseño original no tenía, porque RDS la exige.
5. Inconsistencias conocidas en `entregado/02` (`docs/CODEMAP.md`, sección 2, y avisos en el propio archivo):
   - menciona las Tablas 4 a 6, que no están en el archivo;
   - habla de 31 controles organizacionales y de 6 en otro punto (la norma tiene 37);
   - da 1,800 y 1,950 personas;
   - cita NIST, CIS y Microsoft sin que figuren en las referencias;
   - hay que verificar que cubra los 93 controles: el texto menciona 31 organizacionales y 25 tecnológicos evaluados, y dice "tres facetas de 31 controles" cuando son cuatro temas.
6. Vigencia. La cuenta está en el plan gratuito con créditos: vence el 2027-05-26 o al agotarse el crédito (EV-E2-01). La evidencia que falte se captura antes. Hay dos presupuestos de alerta (EV-E2-10).

## 5. Reglas del curso y formato

Reglas de contenido:

- No fabricar evidencia, resultados, pruebas ni referencias, ni alterar capturas para aparentar una implementación inexistente (`00:571-608`). Hay que poder sustentar todo en la defensa.
- Separar siempre lo diseñado de lo implementado (`00:187`, `01:78`). Si algo no se ejecutó, se escribe "diseñado". Los componentes solo diseñados están en `01_inventario_ambiente_aws.md`, sección 5.
- Toda evidencia se identifica y se liga al elemento que prueba (`00:540`). Las capturas llevan número, título y explicación (`01:148`).
- Sin contraseñas, tokens, claves, secretos ni datos personales reales (`00:542`). Las capturas existentes ya enmascaran el ID de cuenta, IP, DNS, endpoints y correos; cualquier captura nueva se enmascara igual.
- Los estándares se aplican al escenario, no se definen en abstracto (`00:106-107`), y no se copia texto normativo ni se copian definiciones (`02:24`, `01:149`).
- Nomenclatura de la edición 2022 de ISO/IEC 27001 y 27002 (`02:50`).
- Trazabilidad entre activos, procesos, riesgos, controles y resultados: es el criterio que separa "Excelente" de "Satisfactorio" en la rúbrica (`00:563`).
- La IA puede apoyar, pero cada integrante verifica referencias y configuraciones y debe poder defender el contenido; si el docente lo pide, se declaran las herramientas usadas (`00:586-612`).

Formato obligatorio del documento final (`00:506-514`):

| Aspecto | Requisito |
|---|---|
| Papel | Carta; una sola cara por hoja si se imprime |
| Tipografía | Arial 12, estilo normal |
| Interlineado | 1.0 en el cuerpo |
| Sangría | Primera línea, unos cinco espacios |
| Márgenes | Izquierdo 3.5 cm, derecho 2.5 cm, superior 3 cm, inferior 3 cm |
| Numeración | Todas las páginas excepto portada y tabla de contenido; números arábigos, esquina superior derecha |
| Citas y referencias | APA 7.ª edición, versión en español cuando corresponda |

Por confirmar con el docente: el tamaño de letra en tablas y pies de figura, si los títulos pueden ir en negrita (el enunciado dice "estilo normal"), y el interlineado fuera del cuerpo.

## 6. Checklist antes de entregar

- [ ] El texto describe AWS en todo el documento; no queda Azure salvo en una nota de equivalencias si se decide incluirla.
- [ ] Cada activo del inventario aparece en la arquitectura, y cada proceso del BIA apunta a sus activos.
- [ ] Todo riesgo tiene tratamiento, control, responsable, plazo y riesgo residual; todo control de la matriz apunta a un riesgo.
- [ ] La SoA cubre los 93 controles, es coherente con alcance, riesgo y brechas, y justifica cada exclusión.
- [ ] RTO y RPO son los mismos en BIA, riesgos y plan de continuidad; la brecha de RPO está tratada, no ignorada.
- [ ] Cada captura y salida de prueba tiene número, título, explicación y enlace al elemento que prueba; nada se presenta como implementado si no lo está.
- [ ] No hay secretos, ID de cuenta completos, IP públicas, correos ni datos personales reales.
- [ ] Los 20 apartados de resultados (`00:464-483`) y las seis preguntas de discusión están presentes.
- [ ] Formato de la sección 5 aplicado (portada y tabla de contenido sin número de página).
- [ ] Cada cita tiene su referencia en APA 7, con fuente verificada; las referencias citadas en `entregado/02` (NIST, CIS, Microsoft) se completaron.
- [ ] El checklist del enunciado (`00:650-702`) se revisó punto por punto, y lo que no está implementado se declara como diseñado.
- [ ] Presentación con los 14 puntos (`00:620-635`) y duración confirmada con el docente.
- [ ] Todos los integrantes pueden explicar cualquier parte del proyecto.
