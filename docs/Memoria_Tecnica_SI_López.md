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

**[Tema 1	3](#tema-1)**

[**Tema 2	3**](#tema-2)

[**Tema 3	3**](#tema-3)

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

