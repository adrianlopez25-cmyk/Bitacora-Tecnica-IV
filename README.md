# Bitácora Técnica IV. Laboratorio de Teletransportación Digital (SSH y RDP)
## 1.Objetivo principal
El objetivo principal es la implementación y configuración de servicios de acceso remoto (SSH y RDP/Web) sobre un entorno contenedorizado utilizando Docker.
## 2. Requisitos Previos
-Docker Desktop instalado y en funcionamiento.
-Docker Compose.
-Cliente SSH (Terminal, PowerShell o Git Bash).
-Navegador web o cliente RDP (MSTSC / Remmina).
## 3. Instalacion
1-He clonado el docker-compose que aparecia en el punto 6.
2- He subido los contenedores de este archivo gracias a docker-compose up -d.
3- luego he comprobado que los servicios estuvieran activo con: docker ps.
## 4. Configuración Técnica:
1- He generado mi identidad utilizando el correo de campuscamara y el algoritmo de ed25519
2- He copiado la llave publica del ccontenedor.
3- He probado si me dejaba entrar sin tener que introducir mas la contraseña y fue un exito
## 5. Problemas Encontrados y Soluciones
Mi principal problema ha sido a la hora de intentar acceder al ssh alumno@localhost -p 2222. y alssh alumno@127.0.0.1 -p 2222, ya que la primera era normal que no me dejara acceder, pero ni con la segunda me funcionaba.
Finalmente pese a eliminar toda la informacion del docker en clases, he realizado de nuevo el ejercicio en mi pc personal y ahora si me ha dejado poder acceder a todo sin ningun problema.
##6. Reflexion acotada
Finalmente considero que ssh es un pilar clave sobre todo en eficiencia,seguridad y automatización.
