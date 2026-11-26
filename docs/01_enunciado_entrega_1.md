# Enunciado de la Entrega 1

> Fuente: enunciado de la entrega, pegado por el usuario. Copiado sin cambios de contenido.

Presentar el diseño inicial del Sistema de Gestión de Seguridad de la Información para una universidad ficticia, integrando el contexto organizacional, el alcance del SGSI, la arquitectura tecnológica, el inventario de activos y el análisis de impacto al negocio.

Este entregable será la base para desarrollar posteriormente el análisis de riesgos, la selección de controles, las políticas de seguridad, la continuidad y la implementación tecnológica.

## Instrucciones

Cada grupo deberá diseñar una universidad ficticia ubicada en Guatemala. El escenario debe ser suficientemente detallado y coherente con una institución de educación superior que utiliza una arquitectura de nube híbrida.

La organización deberá seleccionar Microsoft Azure, Amazon Web Services o Google Cloud Platform como proveedor de nube pública.

## Contenido obligatorio

## 1. Descripción del escenario

Incluir:

- Nombre de la universidad ficticia.
- Ubicación en Guatemala.
- Cantidad aproximada de estudiantes y colaboradores.
- Facultades, sedes o áreas principales.
- Servicios académicos y administrativos.
- Usuarios internos y externos.
- Principales necesidades de seguridad.
- Problema que pretende resolver el proyecto.

## 2. Contexto y alcance del SGSI

Definir claramente:

- Procesos que formarán parte del SGSI.
- Sistemas, áreas, sedes y servicios incluidos.
- Elementos que quedarán fuera del alcance.
- Justificación del alcance seleccionado.
- Partes interesadas y sus necesidades.
- Requisitos legales, contractuales y académicos aplicables.
- Estándares y marcos que se utilizarán durante el proyecto.

No es suficiente enumerar los estándares. Deben explicar para qué utilizarán cada uno dentro del proyecto.

## 3. Diseño de la arquitectura tecnológica

Presentar un diagrama legible que incluya, según corresponda:

- Infraestructura local.
- Plataforma de nube seleccionada.
- Servidores y bases de datos.
- Sistemas académicos y administrativos.
- Routers, switches y firewall.
- DMZ.
- Segmentación de red.
- Usuarios internos, externos y remotos.
- IAM y autenticación multifactor.
- Sistemas de respaldo.
- Monitoreo y registro de eventos.
- Redundancia y disponibilidad.
- Conexión segura entre la infraestructura local y la nube.

El grupo deberá explicar los componentes, los flujos de comunicación y las principales decisiones del diseño.

## 4. Avance del ambiente tecnológico

Presentar evidencias iniciales de los componentes que ya fueron creados o configurados. Pueden incluir:

- Redes y subredes.
- Máquinas virtuales.
- Servicios en la nube.
- Usuarios, grupos y roles.
- IAM y MFA.
- Reglas de acceso.
- Configuración del firewall.
- Almacenamiento o respaldo.
- Registros y monitoreo.

Se debe diferenciar claramente entre los componentes que solamente fueron diseñados y aquellos que ya se encuentran implementados. No se aceptarán capturas sin identificación y explicación.

## 5. Inventario de activos

El inventario deberá contener como mínimo:

- Identificador.
- Nombre del activo.
- Tipo de activo.
- Descripción.
- Propietario.
- Custodio.
- Ubicación.
- Información procesada.
- Confidencialidad.
- Integridad.
- Disponibilidad.
- Criticidad.
- Dependencias.

Se deberán registrar como mínimo 15 activos relevantes, incluyendo información, sistemas, infraestructura, servicios, personas y proveedores.

## 6. Business Impact Analysis — BIA

Seleccionar como mínimo cinco procesos críticos de la universidad. Por ejemplo:

- Inscripción y asignación de cursos.
- Registro de calificaciones.
- Plataforma educativa virtual.
- Pagos y facturación.
- Gestión de expedientes estudiantiles.
- Correo institucional.
- Biblioteca virtual.

Para cada proceso deberán analizar:

- Descripción del proceso.
- Responsable.
- Sistemas y activos que lo soportan.
- Impacto operativo.
- Impacto financiero.
- Impacto académico.
- Impacto legal o regulatorio.
- Impacto reputacional.
- Tiempo máximo tolerable de interrupción.
- RTO.
- RPO.
- Dependencias.
- Prioridad de recuperación.

## 7. Conclusiones del avance

El grupo deberá explicar:

- Cuáles son los activos más críticos.
- Qué procesos requieren mayor disponibilidad.
- Cuáles son las principales debilidades identificadas.
- Qué aspectos deberán atenderse en las siguientes fases.
- Qué cambios realizaron al diseño después de analizar los activos y el BIA.

## Estructura del documento

Portada. Tabla de contenido. Introducción. Descripción de la organización. Contexto y alcance del SGSI. Partes interesadas. Estándares y marcos seleccionados. Diagrama y explicación de la arquitectura. Evidencias del ambiente tecnológico. Inventario de activos. Business Impact Analysis. Conclusiones. Referencias. Anexos.

## Consideraciones importantes

- Todo el contenido deberá corresponder a la misma universidad ficticia.
- Los activos del inventario deberán aparecer en la arquitectura cuando corresponda.
- Los procesos incluidos en el BIA deberán relacionarse con los activos inventariados.
- No deberán incluirse contraseñas, tokens, claves ni datos personales reales.
- Las capturas deberán llevar número, título y explicación.
- No se aceptarán definiciones copiadas de los estándares sin aplicación al escenario.
- Las fuentes utilizadas deberán citarse de acuerdo con APA, séptima edición.
- Este documento deberá conservarse y mejorarse, porque formará parte del proyecto final.
