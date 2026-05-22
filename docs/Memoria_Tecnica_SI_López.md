#  

# 

# 

# 

# 

# 

# **Memoria Técnica**

**Autor**: Adrián López  
**Ciclo**: Desarrollo de aplicaciones web  
**Módulo**: Sistemas informáticos  
**Fecha**: 15/05/2026  
**ÍNDICE**
[1. Tema 1: Análisis de Necesidades](#1-tema-1-análisis-de-necesidades)
    * [1.1. Contexto y Problemática Actual](#11-contexto-y-problemática-actual)
    * [1.2. Solución Propuesta: Infraestructura Híbrida Docker-Guacamole](#12-solución-propuesta-infraestructura-híbrida-docker-guacamole)
    * [1.3. Justificación Técnica y Beneficios (TCO)](#13-justificación-técnica-y-beneficios-tco)
* [2. Tema 2: Estimación de Costes de Infraestructura y Operaciones (TCO)](#2-tema-2-estimación-de-costes-de-infraestructura-y-operaciones-tco)
    * [2.1. Análisis Avanzado de Escalabilidad y Elasticidad](#21-análisis-avanzado-de-escalabilidad-y-elasticidad)
* [3. Tema 3: Estrategia de Despliegue y Comunicación](#3-tema-3-estrategia-de-despliegue-y-comunicación)
    * [3.1. Flujo Técnico de Despliegue y Protocolo Seguro](#31-flujo-técnico-de-despliegue-y-protocolo-seguro)
    * [3.2. Gestión de Alertas y Mensajería entre Desarrolladores](#32-gestión-de-alertas-y-mensajería-entre-desarrolladores)
* [4. Tema 4: Justificación Científica](#4-tema-4-justificación-científica)
* [5. Referencias](#5-referencias)

# Tema 1 {Analisis de necesidades}
## 1.1. Contexto y Problemática Actual
La empresa objeto de esta intervención técnica, una startup emergente dedicada al desarrollo
multiplataforma, se enfrentaba a una arquitectura de red obsoleta y vulnerable. El equipo de desarrollo
necesitaba acceder de forma recurrente a servidores de bases de datos y entornos de staging ubicados en
un centro de datos remoto. No obstante, la operativa inicial dependía de la apertura indiscriminada de
múltiples puertos en el firewall corporativo para permitir tráfico directo mediante protocolos RDP y SSH.
Esta situación generaba una superficie de ataque excesivamente amplia, exponiendo servicios críticos a
intentos de intrusión por fuerza bruta y vulnerabilidades de día cero. Por consiguiente, se observaba una
falta de control centralizado sobre quién accedía a qué recurso y en qué momento, dificultando las tareas
de auditoría y cumplimiento de normativas de seguridad de la información.
## 1.2. Solución Propuesta: Infraestructura Híbrida Docker-Guacamole
Tras realizar un análisis exhaustivo de los requerimientos de accesibilidad y seguridad, se ha determinado
la implementación de una solución de acceso "clientless" basada en Apache Guacamole, orquestada
mediante la tecnología de contenedores Docker Compose. Esta arquitectura híbrida permite transformar la
gestión de la infraestructura de la siguiente manera:
Centralización del Acceso: Se establece un único punto de entrada a través de un navegador web
estándar (puertos 443/8080), eliminando la necesidad de instalar software cliente en los equipos
locales de los técnicos.
Aislamiento de Servicios: Cada componente (PostgreSQL para la persistencia, Guacamole para el
túnel y los servidores SSH de destino) opera en un entorno estanco. Esto evita el conflicto de
dependencias y asegura que un fallo en un servicio no comprometa la integridad del host.
Seguridad por Diseño: La solución permite cerrar todos los puertos de administración directa en el
firewall, dejando únicamente expuesta la pasarela de Guacamole, la cual puede ser reforzada con
mecanismos de autenticación multifactor (MFA).
## 1.3. Justificación Técnica y Beneficios (TCO)
La viabilidad de este proyecto se fundamenta en la optimización del TCO (Coste Total de Propiedad). Al
optar por herramientas distribuidas bajo licencias de software libre permisivas (Apache y PostgreSQL), la
organización evita el pago de licencias recurrentes por asiento o por servidor, lo cual es crítico en una fase
de escalado startup.
Asimismo, la portabilidad intrínseca de Docker garantiza que el DRP (Plan de Recuperación ante
Desastres) sea extremadamente ágil. En caso de fallo del hardware físico, la infraestructura completa
puede ser desplegada en un nuevo nodo en cuestión de minutos, garantizando una alta disponibilidad. No
obstante, el mayor beneficio reside en la profesionalización de la documentación: un sistema bien
documentado permite que cualquier técnico pueda heredar la gestión del sistema sin curvas de aprendizaje
prolongadas, cumpliendo así con los estándares de calidad de la ingeniería de software moderna.
# 2. Estimación de Costes de Infraestructura.
<img width="1569" height="895" alt="image" src="https://github.com/user-attachments/assets/42078e7a-3999-467d-8670-99748e59dc58" />
## 2. Estimación de Costes de Infraestructura y Operaciones (TCO)
He realizado una investigacion sobre el coste general del coste del proyecto para poder conocer el coste total para nuestra empresa para calcular el margen de ganancias una vez se lo querramos ofrecer a nuestro clientes.

### 2.1. Análisis Avanzado de Escalabilidad y Elasticidad
Para cumplir con una previsión de crecimiento proactiva, se ha modelado la elasticidad de la arquitectura frente a picos de demanda (ej. campañas comerciales o incrementos de tráfico del 300%):
* **Escalado Horizontal de Cómputo:** Mediante políticas de escalado automático (*Auto Scaling*) en AWS ECS, si la CPU supera el 70%, se instanciarán hasta 4 tareas Fargate adicionales. El coste de cómputo pasaría de 24,60 € a 73,80 € de forma elástica, cobrándose únicamente por segundo de uso.
* **Elasticidad de Red (Egress):** Un incremento de tráfico saliente hasta 1.5 TB mensuales situaría el coste de red en 120,00 € `(=0.08*1500)`.
* **Capa de Almacenamiento:** Al utilizar almacenamiento de objetos (AWS S3), el escalado es infinito y lineal sin penalizaciones de aprovisionamiento previo. He empleado este ya que es el mas económica.

*Nota de control de fórmulas: he realizado todo con formas de sumatorios, para que en caso de que se modifique algun dato se actualize esta tabla de forma automatica.

---

## 3. Estrategia de Despliegue y Comunicación

### 3.1. Flujo Técnico de Despliegue y Protocolo Seguro 
Para mover nuestra aplicación desde el ordenador local (entorno de desarrollo) hasta el servidor en la nube (entorno de producción), utilizaremos un flujo automatizado basado en **Git** y el protocolo seguro **SFTP (Secure File Transfer Protocol)**. 

Se descarta por completo el uso del protocolo FTP tradicional. La razón es que FTP transmite los usuarios, las contraseñas y los archivos en texto plano (sin cifrar). Si un atacante interceptara nuestra red, podría robarnos las credenciales fácilmente. 

El flujo exacto que seguirá nuestro código consta de tres pasos:
1. **Control de Versiones (Git):** El desarrollador sube los cambios de código desde su PC haciendo `git push` hacia el repositorio remoto (GitHub).
2. **Conexión Segura (SFTP/SSH):** GitHub Actions (o el desarrollador de forma manual) abre una conexión directa con el servidor web utilizando **SFTP a través del puerto TCP 22**. Al usar este puerto, la conexión se realiza bajo el protocolo SSH.
3. **Cifrado de Datos:** Toda la comunicación, contraseñas y archivos viajan completamente cifrados de extremo a extremo. Esto garantiza la **confidencialidad** (nadie puede leer el código mientras viaja por internet) y la **integridad** (nadie puede modificar el código a mitad de camino), logrando un despliegue 100% seguro.

### 3.2. Gestión de Alertas y Mensajería entre Desarrolladores
Para coordinarnos como equipo de desarrollo y enterarnos al instante si el servidor se cae o falla, integraremos la herramienta de mensajería corporativa **Slack**. 

No podemos depender de que un desarrollador se dé cuenta de un fallo mirando el navegador de vez en cuando; el proceso debe ser automático:
* **El Monitor:** Configuraremos un servicio externo de monitorización que "visita" nuestra web automáticamente cada minuto para comprobar que devuelve un código de estado correcto (HTTP 200 OK).
* **La Alerta (Webhook):** Si el servidor se cae (da un error HTTP 500 o no responde), el monitor enviará un mensaje automático en formato de texto estructurado (**JSON**) hacia un enlace especial de Slack llamado *Incoming Webhook*.
* **Notificación en Slack:** Este mensaje llegará instantáneamente a nuestro canal de chat de equipo llamado `#alertas-servidor`. La alerta avisará a los programadores del equipo mediante una notificación push en el móvil o PC, indicando la hora exacta del fallo y el tipo de error. Así, el equipo podrá comunicarse por el mismo chat y solucionar la incidencia rápidamente.
---

## 4. Justificación Científica

Para justificar la elección de la tecnología de persistencia de datos en mi proyecto, he realizado una investigación en buscadores académicos especializados (Dialnet / Google Académico). El objetivo fue contrastar el rendimiento y la seguridad de las bases de datos relacionales tradicionales frente a los sistemas NoSQL orientados a documentos en aplicaciones web modernas. 

La conclusión principal del artículo científico seleccionado demuestra que, aunque las bases de datos NoSQL como MongoDB ofrecen una gran velocidad en la lectura de datos masivos no estructurados, las bases de datos relacionales como **PostgreSQL** siguen siendo la opción óptima para aplicaciones que requieren una alta integridad de los datos. La investigación concluye que PostgreSQL, gracias a su estricto cumplimiento de las propiedades ACID (Aislamiento, Consistencia, Inmutabilidad y Durabilidad), garantiza que las transacciones y las relaciones entre tablas (claves primarias y foráneas) no sufran corrupciones ni pérdidas de información ante accesos concurrentes de usuarios.[1]

Este estudio apoya directamente mi proyecto, ya que la aplicación maneja lógica de negocio crítica (como registros de usuarios, autenticación y transacciones) donde asegurar que los datos estén perfectamente estructurados, relacionados y sin errores es mucho más prioritario que la flexibilidad extrema que ofrecen los modelos NoSQL.

<img width="839" height="680" alt="image" src="https://github.com/user-attachments/assets/ab1c02ea-4c78-40dc-b642-d7f419c18afc" />


Para apoyar el estudio tambien he revisado la web de amazon [2], en ambos articulos coinciden en que PostgreSQL es superior en cuento a prioridad absoluta en la fiablidad de las relaciones y las transacciones. Además de que destacan que PostgreSQL es ideal para sistemas financieros,registros complejos y plataformas de datos estructurados. Por ultimo indican que el uso de MongoDB seria  solo para datos caoticos o cambiantes en el tiempo, como el uso de un catalogo de productos con carateristicas muy diversas). Todo esto se puede ver reflejado en los diversos gráficos.

---

## Referencias

[1] J. M. García-Luna y A. Martínez-Suárez, "Evaluación de rendimiento y consistencia en sistemas de bases de datos relacionales y NoSQL para aplicaciones web concurrentes," *Revista de Tecnologías de la Información y Computación*, vol. 12, no. 1, pp. 45-58, 2024. Disponible en: https://dialnet.unirioja.es/servlet/articulo?codigo=10041784. [Accedido: 22-may-2026].

[2] Amazon Web Services, "¿Cuál es la diferencia entre MongoDB y PostgreSQL?," aws.amazon.com, 2026. [En línea]. Disponible en: https://aws.amazon.com/es/compare/the-difference-between-mongodb-and-postgresql/. [Accedido: 22-may-2026].
