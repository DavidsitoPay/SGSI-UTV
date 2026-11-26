# Proyecto del curso: Estándares de Seguridad

**Universidad Mariano Gálvez de Guatemala — Facultad de Ingeniería en Sistemas de Información y Ciencias de la Computación**

> Fuente: `Proyecto_Final.pdf` (enunciado oficial del curso). Convertido a Markdown sin cambios de contenido.

**Nombre del proyecto:** Implementación de un Sistema de Gestión de Seguridad de la Información (SGSI).

## Descripción del proyecto

El proyecto consiste en diseñar e implementar un SGSI que permita garantizar la integridad, confidencialidad y disponibilidad de la información, brindando confianza tanto a clientes como a proveedores.

Se tomará en cuenta un enfoque basado en riesgos, siguiendo estándares internacionales de seguridad informática ampliamente aceptados.

## Proyecto final del curso: Estándares de Seguridad

Diseño e Implementación de un Sistema de Gestión de Seguridad de la Información (SGSI)

## 1. Datos generales

- **Curso:** Estándares de Seguridad
- **Programa:** Maestría en Seguridad Informática
- **Actividad:** Proyecto Final
- **Modalidad:** Proyecto aplicado
- **Entrega:** Décima semana del curso
- **Modalidad fin de semana:** Clases virtuales con participación de los Maestrandos

## 2. Enunciado general

El proyecto final del curso consiste en el **diseño e implementación de un Sistema de Gestión de Seguridad de la Información (SGSI)** para una organización perteneciente a uno de los sectores establecidos en este documento.

El proyecto deberá demostrar la capacidad del maestrando para analizar un escenario organizacional, identificar y valorar los activos de información, determinar los riesgos de seguridad, establecer mecanismos de tratamiento y diseñar una arquitectura tecnológica que permita proteger la información y garantizar la continuidad de los servicios críticos.

El desarrollo deberá utilizar un **enfoque basado en riesgos** y aplicar estándares, marcos de referencia y buenas prácticas internacionales relacionados con la seguridad de la información, continuidad del negocio, gobierno de TI, gestión de servicios e infraestructura tecnológica.

El proyecto deberá integrar los aspectos técnicos, administrativos y organizacionales de la seguridad de la información, evitando que los estándares sean utilizados únicamente como elementos teóricos. Cada estándar seleccionado deberá estar relacionado con actividades, controles, decisiones o resultados concretos dentro del escenario planteado.

## 3. Sector permitido

El proyecto deberá desarrollarse para una organización Relacionada con la Educación (Universidad Ficticia).

El escenario podrá corresponder a:

- Una organización ficticia diseñada por el maestrando.
- Una organización real, siempre que se cuente con autorización para utilizar la información necesaria.

Cuando se utilice una organización ficticia, deberá describirse suficientemente su tamaño, estructura, procesos, usuarios, servicios tecnológicos y necesidades de seguridad.

## 4. Arquitectura permitida

**Nube híbrida con soporte para dispositivos móviles, tables, computadores, etc.**

La solución deberá integrar infraestructura local con servicios de nube pública y contemplar mecanismos de seguridad para los dispositivos indicados.

La arquitectura deberá justificarse de acuerdo con las características, necesidades y riesgos del escenario.

## 5. Plataformas de nube

Para proyectos que utilicen nube pública o arquitectura híbrida, deberá seleccionarse una de las siguientes plataformas:

- Microsoft Azure.
- Amazon Web Services (AWS).
- Google Cloud Platform (GCP).

La plataforma seleccionada deberá utilizarse para implementar o demostrar los componentes tecnológicos definidos en la arquitectura.

## 6. Objetivo general

Diseñar e implementar un Sistema de Gestión de Seguridad de la Información para una organización del sector establecido, mediante un enfoque basado en riesgos y la aplicación de estándares internacionales de seguridad, continuidad, gobierno y gestión de servicios de TI, con el propósito de proteger la confidencialidad, integridad y disponibilidad de la información y fortalecer la resiliencia de los servicios tecnológicos críticos de la organización.

## 7. Objetivos específicos

El proyecto deberá permitir al maestrando:

1. Identificar y clasificar los activos de información, tecnológicos y organizacionales que forman parte del alcance del SGSI.
2. Analizar los procesos críticos de la organización mediante un Business Impact Analysis (BIA).
3. Identificar amenazas, vulnerabilidades y escenarios de riesgo que puedan afectar los activos y procesos críticos.
4. Analizar y evaluar los riesgos mediante metodologías y buenas prácticas reconocidas internacionalmente.
5. Diseñar una arquitectura tecnológica que incorpore mecanismos de seguridad, segmentación, redundancia, monitoreo y recuperación.
6. Seleccionar controles de seguridad alineados con ISO/IEC 27001 e ISO/IEC 27002.
7. Aplicar principios de Zero Trust para el control de acceso a recursos y servicios.
8. Incorporar mecanismos de detección, monitoreo y respuesta ante incidentes de seguridad.
9. Diseñar estrategias de continuidad del negocio y recuperación ante desastres.
10. Aplicar principios de gobierno y gestión de servicios de TI mediante COBIT 2019 e ITIL 4.
11. Establecer buenas prácticas para la infraestructura del Data Center tomando como referencia TIA-942.
12. Demostrar mediante evidencias la implementación o configuración de los controles tecnológicos seleccionados.

## 8. Estándares y marcos de referencia

El proyecto deberá considerar, como mínimo, los siguientes estándares y marcos:

| Estándar / Marco | Aplicación esperada |
|---|---|
| ISO/IEC 27001 | Sistema de Gestión de Seguridad de la Información |
| ISO/IEC 27002 | Controles de seguridad |
| ISO/IEC 27005 | Gestión de riesgos de seguridad de la información |
| NIST SP 800-30 | Evaluación de riesgos |
| OCTAVE | Evaluación y gestión del riesgo |
| NIST Cybersecurity Framework | Gestión del riesgo y ciberseguridad |
| Zero Trust Architecture | Control de acceso y seguridad de arquitectura |
| ISO 22301 | Continuidad del negocio |
| COBIT 2019 | Gobierno y gestión de TI |
| ITIL 4 | Gestión de servicios de TI |
| TIA-942 | Infraestructura y Data Center |

El maestrando deberá demostrar cómo se aplica cada estándar seleccionado al escenario.
No se permitirá presentar definiciones teóricas, sino como lo implementó.

## 9. Fases del proyecto

### FASE 1. Diseño de infraestructura

**Objetivo:** Diseñar la arquitectura tecnológica y de seguridad que soportará el SGSI.

**Deberá incluir:**

- Servidores.
- Bases de datos.
- Sistemas de almacenamiento.
- Switches.
- Routers.
- Firewalls NGFW.
- IDS/IPS.
- DMZ.
- Segmentación de red.
- Virtualización.
- Contenedores, cuando corresponda.
- IAM.
- MFA.
- Zero Trust.
- SIEM.
- Sistemas de respaldo.
- Redundancia.
- Alta disponibilidad.
- Continuidad del negocio.
- Recuperación ante desastres.

**Entregable — E1 Documento de diseño de infraestructura.** Deberá contener:

1. Descripción del escenario.
2. Diagrama de arquitectura.
3. Descripción de componentes.
4. Flujos de comunicación.
5. Segmentación de red.
6. Controles de seguridad.
7. Mecanismos de redundancia.
8. Estrategia inicial de continuidad y recuperación.
9. Justificación técnica de la solución.

**Aprobación:** El diagrama deberá ser presentado al docente para aprobación **una semana después de la asignación del proyecto**.

La aprobación del diseño será requisito para continuar con la construcción del ambiente.

### FASE 2. Construcción del ambiente aprobado

Una vez aprobado el diseño, el maestrando deberá construir una implementación funcional o demostrable de la solución seleccionada.

**Deberá demostrar, según corresponda:**

- Redes.
- Subredes.
- Segmentación.
- Servicios cloud.
- Servidores.
- Aplicaciones.
- Bases de datos.
- IAM.
- MFA.
- Controles de acceso.
- Seguridad perimetral.
- Monitoreo.
- Registro de eventos.
- Backup.
- Recuperación.

**Entregable — E2 Ambiente tecnológico implementado.** Deberá incluir:

- Descripción de la implementación.
- Evidencias técnicas.
- Capturas de configuración.
- Direccionamiento y segmentación.
- Servicios implementados.
- Controles configurados.
- Pruebas realizadas.
- Resultados obtenidos.

El maestrando deberá diferenciar claramente entre componentes **diseñados** y componentes **efectivamente implementados**.

### FASE 3. Diseño del modelo de gestión de seguridad

En esta fase se establecerá formalmente el modelo de seguridad de la organización.

**Deberá incluir:**

- Alcance del SGSI.
- Contexto de la organización.
- Activos.
- Procesos críticos.
- Gestión de riesgos.
- Controles.
- Políticas.
- Zero Trust.
- Gestión de incidentes.
- Continuidad.
- Gobierno de TI.
- Gestión de servicios.

**Entregable — E3 Modelo de gestión de seguridad de la información.**

### FASE 4. Implementación y gestión de riesgos

Esta fase constituye uno de los componentes principales del proyecto.

#### 4.1 Inventario de activos

Deberá elaborarse un inventario que incluya como mínimo:

- Identificador.
- Activo.
- Tipo.
- Propietario.
- Custodio.
- Ubicación.
- Información procesada.
- Confidencialidad.
- Integridad.
- Disponibilidad.
- Criticidad.
- Dependencias.

**Entregable — E4.1 Inventario de activos.**

#### 4.2 Business Impact Analysis — BIA

Deberán identificarse los procesos críticos y determinarse los impactos derivados de su interrupción.

Se deberá considerar:

- Impacto operativo.
- Impacto financiero.
- Impacto reputacional.
- Impacto legal o regulatorio.
- Impacto académico o de negocio.
- RTO.
- RPO.
- MTPD.

**Entregable — E4.2 BIA.**

#### 4.3 Análisis de riesgos

El análisis deberá realizarse utilizando como referencia NIST SP 800-30.

Como mínimo deberá contemplar:

- Activo.
- Amenaza.
- Vulnerabilidad.
- Probabilidad.
- Impacto.
- Riesgo inherente.
- Controles existentes.
- Riesgo residual.

**Entregable — E4.3 Matriz de análisis de riesgos.**

#### 4.4 Evaluación mediante OCTAVE

Deberá aplicarse el modelo OCTAVE de manera coherente con el escenario.

El maestrando deberá explicar:

- Metodología utilizada.
- Activos críticos.
- Amenazas.
- Escenarios de riesgo.
- Evaluación.
- Resultados.

**Entregable — E4.4 Evaluación OCTAVE.**

#### 4.5 Matriz de calor

Deberá elaborarse una matriz de riesgo utilizando como mínimo: **Probabilidad × Impacto**.

El maestrando deberá definir claramente los criterios utilizados para clasificar los niveles de riesgo.

**Entregable — E4.5 Matriz de calor.**

#### 4.6 Plan de tratamiento

Cada riesgo deberá contar con una estrategia de tratamiento:

- Mitigar.
- Evitar.
- Transferir.
- Aceptar.

El plan deberá identificar:

- Riesgo.
- Tratamiento.
- Control.
- Responsable.
- Prioridad.
- Plazo.
- Estado.
- Riesgo residual esperado.

**Entregable — E4.6 Plan de tratamiento de riesgos.**

### FASE 5. Políticas, controles y buenas prácticas

El maestrando deberá desarrollar las políticas necesarias para el escenario seleccionado.

**Políticas mínimas:**

**Dominio e identidad**

- Administración de identidades.
- Autenticación.
- Autorización.
- MFA.
- Privilegios.

**Grupos**

- Administradores.
- Usuarios.
- Personal académico.
- Personal administrativo.
- Terceros.

**Equipos**

- Hardening.
- Gestión de parches.
- EDR.
- Cifrado.
- Control de aplicaciones.

**Usuarios**

- Contraseñas.
- MFA.
- Mínimo privilegio.
- Acceso remoto.
- Uso aceptable.

**Nube**

- Control de acceso.
- Configuración segura.
- Segmentación.
- Registro.
- Monitoreo.

**Dispositivos móviles**

- MDM.
- DLP.
- Cifrado.
- Bloqueo.
- Borrado remoto.
- BYOD.

**Entregables:**

- E5.1 Políticas de seguridad.
- E5.2 Matriz de controles.
- E5.3 Documento de buenas prácticas.

Cada control deberá relacionarse con el riesgo que pretende tratar.

### FASE 6. Gobernanza y gestión de servicios de TI

El maestrando deberá aplicar COBIT 2019 e ITIL 4 al escenario.

**COBIT 2019** — Deberá considerar aspectos relacionados con:

- Gobierno.
- Gestión de riesgos.
- Cumplimiento.
- Alineamiento estratégico.
- Gestión de recursos.
- Desempeño.

**ITIL 4** — Deberá considerar, según corresponda:

- Gestión de incidentes.
- Gestión de cambios.
- Gestión de problemas.
- Gestión de niveles de servicio.
- Gestión de activos.
- Gestión de configuración.
- Gestión de continuidad.
- Gestión de seguridad.

**Entregable — E6 Modelo de gobierno y gestión de servicios de TI.**

### FASE 7. Continuidad del negocio y Data Center

#### 7.1 Continuidad

El estudiante deberá desarrollar:

- Estrategia de continuidad.
- BCP.
- DRP.
- RTO.
- RPO.
- Procedimientos de recuperación.
- Roles y responsabilidades.
- Pruebas de recuperación.

#### 7.2 Data Center

Deberán considerarse buenas prácticas relacionadas con TIA-942:

- Energía.
- UPS.
- Generadores.
- Climatización.
- Cableado.
- Redundancia.
- Seguridad física.
- Control de acceso.
- Protección contra incendios.
- Monitoreo.
- Resiliencia.

**Entregable — E7 Plan de continuidad, recuperación y buenas prácticas del Data Center.**

## 10. Discusión

El documento final deberá incluir una sección de discusión académica entre los maestrandos del grupo que responda las siguientes preguntas:

- **10.1 Zero Trust:** ¿Cuáles son las principales diferencias y consideraciones al implementar Zero Trust en un entorno de nube pública frente a un entorno híbrido?
- **10.2 MDM y DLP:** ¿Cuáles son las principales buenas prácticas para proteger la información institucional mediante MDM y DLP en dispositivos móviles?
- **10.3 Cumplimiento:** ¿Qué consideraciones adicionales deben tomarse en cuenta para cumplir con las normativas locales e internacionales relacionadas con la seguridad de la información y la computación en la nube?
- **10.4 SIEM, EDR y XDR:** ¿Cuál es la contribución de SIEM, EDR y XDR a la detección y respuesta ante incidentes en comparación con mecanismos tradicionales?
- **10.5 ISO/IEC 27001:** ¿Cómo puede mantenerse la mejora continua del SGSI después de una eventual certificación ISO/IEC 27001?
- **10.6 COBIT e ITIL:** ¿Cómo pueden COBIT 2019 e ITIL 4 complementarse para alinear la seguridad de la información y la gestión de TI con los objetivos organizacionales?

Las respuestas deberán estar sustentadas mediante fuentes académicas, técnicas o normativas confiables.

## 11. Documento final

El documento deberá cumplir con la siguiente estructura:

- Portada
- Tabla de contenido
  1. Introducción
  2. Marco teórico
  3. Metodología
  4. Resultados
  5. Discusión
  6. Conclusiones
  7. Referencias
  8. Anexos

## 12. Contenido mínimo de resultados

El capítulo de resultados deberá incluir:

1. Descripción del escenario.
2. Alcance del SGSI.
3. Diagrama de infraestructura.
4. Explicación de la arquitectura.
5. Inventario de activos.
6. BIA.
7. Análisis de riesgos.
8. Evaluación OCTAVE.
9. Matriz de calor.
10. Plan de tratamiento.
11. Políticas de seguridad.
12. Matriz de controles.
13. Buenas prácticas.
14. Zero Trust.
15. MDM/DLP.
16. SIEM/EDR/XDR.
17. Implementación tecnológica.
18. Continuidad y recuperación.
19. COBIT/ITIL.
20. Data Center.

## 13. Cronograma de entregas

El cronograma deberá adaptarse a la modalidad del curso.

| Semana | Actividad | Entregable |
|---|---|---|
| 1 | Asignación del proyecto | Enunciado y selección del escenario |
| 2 | Diseño conceptual | E1 Arquitectura y diagrama |
| 3 | Aprobación y construcción | E2 Ambiente tecnológico |
| 4 | SGSI y activos | E3 + E4.1 |
| 5 | BIA | E4.2 |
| 6 | Análisis de riesgos | E4.3 + E4.4 |
| 7 | Matriz y tratamiento | E4.5 + E4.6 |
| 8 | Controles y políticas | E5 |
| 9 | Gobierno, continuidad y Data Center | E6 + E7 |
| 10 | Entrega final y defensa | Documento final + presentación |

## 14. Formato obligatorio

El documento final deberá cumplir con:

- **Papel:** tamaño carta; impresión o presentación de una sola cara por hoja, cuando corresponda.
- **Tipografía:** Arial, tamaño 12, estilo normal.
- **Interlineado:** 1.0 para el cuerpo del documento.
- **Sangría:** de primera línea de aproximadamente cinco espacios.
- **Márgenes:** izquierdo 3.5 cm; derecho 2.5 cm; superior 3 cm; inferior 3 cm.
- **Numeración:** todas las páginas deberán estar numeradas, excepto la portada y la tabla de contenido. La numeración deberá ser arábiga y ubicarse en la esquina superior derecha.
- **Referencias:** las citas y referencias deberán elaborarse de acuerdo con **APA, séptima edición**, utilizando la versión en español cuando corresponda.

## 15. Evidencias requeridas

El proyecto deberá presentar evidencias que permitan demostrar la realización de las actividades y, cuando corresponda, la implementación de los controles.

Las evidencias podrán incluir:

- Diagramas.
- Capturas de configuración.
- Tablas.
- Matrices.
- Configuraciones de infraestructura.
- Evidencias de IAM.
- Evidencias de MFA.
- Evidencias de segmentación.
- Evidencias de monitoreo.
- Evidencias de SIEM.
- Evidencias de EDR.
- Evidencias de MDM.
- Evidencias de DLP.
- Evidencias de backup.
- Evidencias de recuperación.
- Resultados de pruebas.
- Evidencias de controles.

Toda evidencia deberá estar identificada y relacionada con el elemento del proyecto que pretende demostrar.

No deberán incluirse contraseñas, tokens, claves, secretos, datos personales reales ni información confidencial de terceros.

## 16. Rúbrica de evaluación

| Criterio | Ponderación |
|---|---|
| Diseño de infraestructura y arquitectura | 15 % |
| Construcción/implementación del ambiente | 10 % |
| Inventario de activos | 5 % |
| BIA | 10 % |
| Análisis y evaluación de riesgos | 15 % |
| Plan de tratamiento y controles | 10 % |
| Políticas, Zero Trust, MDM/DLP y seguridad | 10 % |
| Gobierno y gestión de servicios — COBIT/ITIL | 5 % |
| Continuidad, recuperación y Data Center | 5 % |
| Discusión y análisis crítico | 5 % |
| Calidad del documento, referencias y APA | 5 % |
| **TOTAL SOBRE 20 PUNTOS DEL PF** | **100 %** |

### Niveles de desempeño

**Excelente — 90–100 %.** El proyecto presenta una solución integral, coherente y técnicamente fundamentada. Existe trazabilidad entre activos, procesos, riesgos, controles y resultados. Las implementaciones están respaldadas por evidencias suficientes y los estándares son aplicados de manera pertinente.

**Satisfactorio — 80–89 %.** El proyecto cumple los principales requisitos y presenta una solución funcional y coherente, aunque existen oportunidades de mejora en la profundidad técnica, integración de estándares, evidencias o justificación.

**En desarrollo — 70–79 %.** El proyecto presenta los componentes principales, pero existen inconsistencias, información incompleta, aplicación superficial de estándares o evidencias insuficientes.

**Insuficiente — Menor de 70 %.** El proyecto presenta incumplimientos significativos de los requisitos, ausencia de componentes fundamentales, falta de coherencia entre las diferentes fases o evidencia insuficiente de desarrollo e implementación.

## 17. Criterios de originalidad

El proyecto deberá ser producto del trabajo académico de los maestrandos.

Se considerará una falta académica:

- Presentar como propio material elaborado por terceros.
- Copiar proyectos publicados en Internet.
- Utilizar proyectos de otros estudiantes sin autorización.
- Fabricar evidencias de implementación.
- Alterar capturas o resultados con el propósito de aparentar una implementación inexistente.
- Presentar información técnica que no pueda ser sustentada durante la defensa.

Cuando se utilicen ideas, modelos, imágenes, tablas, código, documentos o información desarrollada por terceros, deberá reconocerse la fuente correspondiente.

## 18. Uso de inteligencia artificial

El uso de herramientas de Inteligencia Artificial generativa podrá emplearse como apoyo al proceso académico, siempre que se respeten los principios de transparencia, responsabilidad y autoría.

La IA podrá utilizarse, por ejemplo, para:

- Generar ideas iniciales.
- Apoyar la investigación.
- Mejorar la redacción.
- Revisar ortografía y gramática.
- Generar ejemplos conceptuales.
- Apoyar la elaboración de estructuras o tablas.

Sin embargo, el maestrando será responsable de:

- Verificar la información generada.
- Validar las referencias.
- Comprender los conceptos utilizados.
- Comprobar las configuraciones técnicas.
- Validar los resultados.
- Defender oralmente el contenido presentado.

No deberá utilizarse IA para fabricar evidencias, resultados, pruebas de implementación o referencias inexistentes.

El docente podrá solicitar al maestrando que explique cualquier componente del proyecto durante la defensa.

Cuando el docente lo solicite, el estudiante deberá declarar las herramientas de IA utilizadas y describir de manera general su propósito dentro del desarrollo del proyecto.

## 19. Presentación y defensa

Cada proyecto deberá ser presentado y defendido ante el docente.

La presentación deberá tener una duración aproximada de **15 a 25 minutos dependiendo del número de grupos**, seguida de una sesión de una pregunta técnica por grupo.

La presentación deberá incluir como mínimo:

1. Organización y problema identificado.
2. Objetivos.
3. Arquitectura.
4. Principales activos.
5. BIA.
6. Principales riesgos.
7. Matriz de riesgos.
8. Controles seleccionados.
9. Implementación.
10. Evidencias.
11. Continuidad.
12. Gobierno de TI.
13. Resultados.
14. Conclusiones.

Durante la defensa, el docente podrá formular preguntas relacionadas con:

- Decisiones de arquitectura.
- Riesgos identificados.
- Justificación de controles.
- Aplicación de estándares.
- Configuración tecnológica.
- Resultados.
- Continuidad.
- Gobierno de TI.

Cada integrante del equipo deberá demostrar conocimiento total del proyecto.

## 20. Lista de verificación final del estudiante

Antes de entregar el proyecto, el maestrando deberá verificar:

**Organización**

- [ ] El sector seleccionado corresponde a uno de los sectores autorizados.
- [ ] La organización está claramente descrita.
- [ ] Se identificaron los procesos críticos.
- [ ] Se identificaron los usuarios y actores.

**Arquitectura**

- [ ] Se seleccionó una arquitectura autorizada.
- [ ] Se justificó la arquitectura.
- [ ] El diagrama está completo.
- [ ] Se identificaron las zonas de seguridad.
- [ ] Se identificó la segmentación.
- [ ] Se incorporaron mecanismos de redundancia.
- [ ] Se documentaron los flujos de comunicación.

**Riesgos**

- [ ] Se elaboró el inventario de activos.
- [ ] Se realizó el BIA.
- [ ] Se identificaron amenazas.
- [ ] Se identificaron vulnerabilidades.
- [ ] Se realizó el análisis de riesgos.
- [ ] Se aplicó OCTAVE.
- [ ] Se elaboró la matriz de calor.
- [ ] Se estableció el tratamiento de riesgos.
- [ ] Se determinó el riesgo residual.

**Seguridad**

- [ ] Se definió el modelo de seguridad de la información.
- [ ] Se establecieron políticas de seguridad.
- [ ] Se implementaron controles de seguridad basados en ISO/IEC 27001 e ISO/IEC 27002.
- [ ] Se aplicaron principios de Zero Trust Architecture (ZTA).
- [ ] Se implementaron mecanismos de gestión de identidad y acceso (IAM).
- [ ] Se estableció autenticación multifactor (MFA).
- [ ] Se implementaron mecanismos de segmentación y control de acceso a la red.
- [ ] Se implementaron mecanismos de protección de endpoints mediante EDR y/o XDR.
- [ ] Se implementaron mecanismos de monitoreo y correlación de eventos mediante SIEM.
- [ ] Se establecieron mecanismos de protección de datos mediante DLP.
- [ ] Se definieron controles para la administración de dispositivos móviles mediante MDM.
- [ ] Se establecieron políticas de seguridad para usuarios, grupos, equipos y dispositivos.
- [ ] Se establecieron controles para la conectividad segura con la nube.
- [ ] Se establecieron controles para la conectividad segura de dispositivos móviles.
- [ ] Se definieron mecanismos de gestión y respuesta ante incidentes de seguridad.
- [ ] Se establecieron mecanismos de respaldo y recuperación de información.
- [ ] Se documentaron las buenas prácticas de seguridad aplicadas al escenario.
- [ ] Se presentaron evidencias de los controles implementados.

---

*Y CONOCERÉIS LA VERDAD, Y LA VERDAD OS HARÁ LIBRES — JUAN 8:22*
