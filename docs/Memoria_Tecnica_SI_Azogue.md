# **Memoria Técnica: Infraestructura de Acceso Remoto Centralizado**

**Autor:** Azogue Castaño Pablo  
**Ciclo:** Desarrollo Aplicaciones Web  
**Módulo**: Sistemas Informáticos  
**Fecha:** 15 de mayo de 2026

**ÍNDICE**

[**Memoria Técnica: Infraestructura de Acceso Remoto Centralizado	1**](#heading=)

[**1\. Análisis de Necesidades	1**](#heading=)

[1.1 Contexto y Problemática Actual	1](#heading=)

[1.2 Solución Propuesta: Ecosistema Docker-Guacamole	1](#heading=)

[1.3 Justificación Técnica y Beneficios (TCO)	2](#heading=)

[**2\.Estimación de Costes de Infraestructura	2**](#heading=)

[**3\.Estrategia de Despliegue y Comunicación**](#heading=)

[**4\.Justificación**](#heading=)

# **1\. Análisis de Necesidades**

## **1.1 Contexto y Problemática Actual**

La infraestructura tecnológica previa de la organización se caracterizaba por un modelo de administración descentralizado y fragmentado, lo cual generaba ineficiencias operativas y riesgos de seguridad críticos. Los técnicos de sistemas requerían acceso frecuente a servidores de bases de datos y entornos de desarrollo ubicados en centros de datos remotos. La solución tradicional consistía en la apertura directa de puertos en el firewall perimetral para protocolos como RDP (Remote Desktop Protocol) y SSH (Secure Shell).  
Esta configuración inicial presentaba una superficie de ataque excesivamente amplia, exponiendo los servicios de administración a ataques de fuerza bruta y escaneos de vulnerabilidades automatizados. Asimismo, la dependencia de clientes pesados instalados en las máquinas locales de los técnicos dificultaba la uniformidad de las herramientas de trabajo y complicaba la auditoría centralizada de las conexiones, impidiendo un control granular sobre quién accedía a qué recurso y en qué momento.

## **1.2 Solución Propuesta: Ecosistema Docker-Guacamole**

Para mitigar estas deficiencias, se ha procedido a la implementación de una arquitectura basada en microservicios orquestados mediante Docker Compose, centrada en el uso de Apache Guacamole. Esta solución funciona como un gateway client-less, lo que significa que el acceso a los recursos internos se realiza exclusivamente a través de un navegador web estándar compatible con HTML5.  
Al centralizar todo el tráfico de administración a través de un único túnel cifrado (HTTPS), la empresa puede cerrar todos los puertos de administración directa al exterior, reduciendo drásticamente la exposición del sistema. La contenedorización mediante Docker aporta, además, un nivel de abstracción y aislamiento esencial: cada componente (la base de datos PostgreSQL para autenticación, el demonio guacd para la transcodificación de protocolos y el servidor web) opera en un entorno estanco, evitando conflictos de dependencias y simplificando los procesos de actualización y parcheado de seguridad.

## **1.3 Justificación Técnica y Beneficios (TCO)**

La elección de esta arquitectura frente a la conexión directa por RDP se fundamenta en la optimización de recursos y la seguridad multicapa. Mientras que RDP directo requiere una gestión compleja de certificados y clientes específicos, la solución propuesta permite una gestión de identidad centralizada. Desde el punto de vista del Coste Total de Propiedad (TCO), el uso de software bajo licencias permisivas (Apache License 2.0) elimina las barreras financieras asociadas a las licencias de acceso remoto propietarias, permitiendo una escalabilidad horizontal sin costes adicionales por usuario.  
Además, la naturaleza de Docker como Infraestructura como Código (IaC) garantiza que el Plan de Recuperación ante Desastres (DRP) sea extremadamente ágil; el entorno completo puede ser recreado en un nuevo nodo en cuestión de minutos. Tal como indica la literatura académica en ingeniería de software (Drake, 2008), un análisis de requisitos y una especificación precisa son determinantes para evitar fallos críticos en entornos de producción. En consecuencia, esta implementación no solo resuelve una necesidad técnica inmediata, sino que establece un estándar de profesionalidad y seguridad alineado con las demandas del sector tecnológico actual.

# **2\.*Estimación de costes de infraestructuras*
<img width="1331" height="369" alt="image" src="https://github.com/user-attachments/assets/f7b94c80-87da-4d09-84fc-b19a3f6ac71e" />

# **3.*Estrategia de Despliegue y Comunicación*

El código se trasladará desde nuestro servidor local hacia el servidor de producción mediante SFTP (SSH File Transfer Protocol).Ya que es el método manual o semiautomático más recomendado. Reemplaza al antiguo FTP (que envía las contraseñas en texto claro) utilizando el protocolo SSH para cifrar toda la comunicación.

**Por qué es seguro:**
 - Cifrado extremo a extremo: Los datos viajan cifrados, impidiendo que sean interceptados.
 - Autenticación robusta: Permite el uso de pares de claves criptográficas  en lugar de contraseñas, lo que elimina los ataques de fuerza bruta.
 - Control de accesos: Se puede configurar para que los usuarios queden "enjaulados" únicamente en el directorio de la aplicación, evitando que accedan al resto del servidor.

#### **3.1 Mensajería**

El equipo trabajará en Discord mediante un canal dedicado a las incidencias. Se creará una automatización para enviar notificaciones a los miembros del canal cuando haya un error.Para ello todos deben tener activadas las notificaciones en sus dispositivos.

# **4.*Estrategia de Despliegue y Comunicación*

La estrategia de centralizar y securizar los servicios de administración mediante Docker. El autor analiza cómo la contenedorización con Docker se ha convertido en una herramienta indispensable para desplegar servicios de red de forma ágil, segura y eficiente. En su estudio, destaca que esta tecnología permite aislar por completo cada servicio (evitando conflictos entre dependencias del sistema) y optimizar el uso del hardware, logrando que entornos complejos funcionen con un consumo mínimo de recursos en comparación con las máquinas virtuales clásicas. Esta investigación avala directamente el diseño de nuestro proyecto, justificando técnicamente el uso de contenedores independientes para el ecosistema Guacamole, lo que garantiza una infraestructura robusta, fácil de mantener y con un coste de computación en la nube reducido.

[1] T. Combe, A. Antony, and R. Di Pietro, "To Docker or Not to Docker: A Security Perspective," IEEE Cloud Computing, vol. 3, no. 5, pp. 54-62, Sept.-Oct. 2016, doi: 10.1109/MCC.2016.100.
