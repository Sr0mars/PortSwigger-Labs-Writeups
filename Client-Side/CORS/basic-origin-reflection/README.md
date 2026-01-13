# 🌐 CORS con Reflexión Básica del Origen

## 🎯 Objetivo
Extraer información sensible (API Key) del perfil de un usuario aprovechando una configuración de CORS extremadamente permisiva.

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** CORS Misconfiguration (Basic Origin Reflection) 🔀
* **Severidad:** Media-Alta 🔴
* **Concepto clave:** El servidor refleja dinámicamente cualquier valor recibido en el encabezado `Origin` y permite el uso de credenciales.

## ⚙️ Explicación Técnica
La aplicación web confía ciegamente en cualquier origen externo al reflejar el encabezado `Origin` de la solicitud en el encabezado de respuesta `Access-Control-Allow-Origin`. Además, al estar configurada con `Access-Control-Allow-Credentials: true`, permite que scripts de sitios terceros realicen peticiones autenticadas y lean la respuesta.

El exploit utiliza JavaScript para realizar una petición `GET` al endpoint `/accountDetails` en nombre del usuario víctima y luego envía el contenido de la respuesta (que incluye la API Key) a un servidor controlado por el atacante.

## 📊 Flujo del Ataque
```mermaid
sequenceDiagram
    participant V as Navegador Víctima
    participant S as Servidor Vulnerable
    participant A as Servidor Atacante

    V->>A: Visita página maliciosa del atacante
    A-->>V: Entrega el script de exploit
    V->>S: GET /accountDetails (Origin: atacante.com + Cookies)
    S-->>V: Respuesta con datos (CORS permite el origen reflejado)
    V->>A: Exfiltración de datos robados vía URL (Base64)
    Note right of A: 🚩 API Key capturada en logs
