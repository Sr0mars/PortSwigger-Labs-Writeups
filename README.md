🛡️ PortSwigger Labs: Writeups & Exploits
Este repositorio contiene una colección de pruebas de concepto (PoCs) y scripts de automatización desarrollados para resolver laboratorios avanzados de PortSwigger Academy. El objetivo es documentar el proceso de identificación, explotación y análisis de vulnerabilidades críticas en entornos web controlados.

🚀 Resumen del Proyecto
Este portafolio demuestra un dominio práctico en diversas categorías de vulnerabilidades, divididas según su impacto y entorno de ejecución:

🌐 Client-Side Attacks
Enfoque en vulnerabilidades que comprometen la sesión y los datos del usuario final mediante la manipulación del navegador.

CORS (Cross-Origin Resource Sharing): Explotación de configuraciones inseguras de origen (Reflection & Null Origin) para exfiltrar datos sensibles.

WebSockets: Secuestro de canales de comunicación bidireccional mediante CSWSH.

HTTP Request Smuggling: Técnicas de desincronización de cliente (CL.0) para capturar cookies de sesión.

XSS to CSRF: Encadenamiento de vulnerabilidades para anular protecciones de tokens y realizar acciones no autorizadas (como cambios de email).

🖥️ Server-Side Attacks
Ataques dirigidos a la lógica del backend y la infraestructura, buscando el control del servidor o la extracción masiva de datos.

Insecure Deserialization: Logro de Ejecución Remota de Comandos (RCE) mediante la manipulación de objetos serializados en PHP (Symfony Gadget Chains).

Blind SQL Injection: Automatización de extracción de bases de datos mediante scripts en Python, utilizando técnicas basadas en:

Respuestas condicionales: Inferencia booleana simple.

Errores condicionales: Forzado de errores 500 en entornos Oracle.

Retardos de tiempo: Uso de pg_sleep para exfiltración en PostgreSQL.

🛠️ Herramientas y Tecnologías
Lenguajes: Python (Requests, Pwntools), JavaScript (XMLHttpRequest, WebSockets), PHP.

Proxies: Burp Suite Professional (Intruder, Repeater, Collaborator).

Gadget Chains: Herramientas como PHPGGC para deserialización.

📊 Metodología
Cada laboratorio incluye:

Exploit Code: Código fuente listo para usar.

Documentación Técnica: Análisis de la causa raíz y flujo del ataque.

Visualizaciones: Diagramas de secuencia para explicar interacciones complejas entre cliente y servidor.
