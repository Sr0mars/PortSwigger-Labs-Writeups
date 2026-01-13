# 🚀 HTTP Request Smuggling: Client-Side Desync

## 🎯 Objetivo
Provocar una desincronización en la conexión HTTP entre el navegador de la víctima y el servidor para capturar cookies de sesión y exfiltrarlas a un área pública (comentarios).

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** Client-Side Desync (CL.0) ⚡
* **Severidad:** Crítica 💀
* **Técnica:** Desincronización de flujo mediante peticiones POST malformadas.

## ⚙️ Explicación Técnica
A diferencia del Request Smuggling tradicional (Server-Side), el **Client-Side Desync** ocurre cuando un servidor no cierra la conexión correctamente tras una petición o interpreta mal el tamaño del cuerpo. 

En este exploit, enviamos una petición mediante `fetch()` que contiene una segunda petición HTTP completa en su cuerpo. El servidor procesa la primera, pero deja la "smuggled request" en el buffer de la conexión. Cuando el navegador realiza la siguiente petición legítima, esta se concatena a nuestra petición maliciosa, provocando que la sesión de la víctima se envíe como parte de un comentario.

## 📊 Flujo del Ataque
```mermaid
sequenceDiagram
    participant B as Navegador Víctima
    participant S as Servidor (Frontend/Backend)
    participant A as Atacante

    B->>S: Envía Payload (Smuggled Request oculta)
    Note over S: El servidor procesa la 1ra petición
    Note over S: La "Smuggled Request" se queda en el buffer
    B->>S: Siguiente petición legítima (con Cookies)
    Note over S: Se concatena con la Smuggled Request
    S-->>A: Procesa como un comentario con la Cookie de la víctima
    Note right of A: 🚩 Cookie capturada en la sección de comentarios
