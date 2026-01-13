# 🧪 Lab: CORS con origen 'null' marcado como confiable

## 🎯 Objetivo
Extraer la **API Key** del administrador aprovechando una configuración de CORS extremadamente permisiva que confía en orígenes nulos.

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** CORS Misconfiguration (Trusted Null Origin) 🔀
* **Severidad:** Alta 🔴
* **Vector:** Uso de `sandbox` en iframes para generar un origen `null`.

## ⚙️ Explicación Técnica
El servidor está configurado para aceptar el encabezado `Origin: null`. En este exploit, utilizamos un `<iframe>` con el atributo `sandbox`. Al usar `sandbox="allow-scripts"`, el navegador procesa el contenido del iframe con un origen **único y opaco**, que se traduce como `null`.

Si el servidor responde con `Access-Control-Allow-Origin: null` y `Access-Control-Allow-Credentials: true`, podemos realizar una petición autenticada desde el iframe y leer la respuesta sensible.

## 📊 Flujo del Ataque
```mermaid
sequenceDiagram
    participant V as Navegador Víctima
    participant S as Servidor Vulnerable
    participant A as Servidor Atacante

    V->>A: Visita página con iframe malicioso
    Note over V: El iframe genera Origin: null
    V->>S: GET /accountDetails (Origin: null + Cookies)
    S-->>V: Respuesta con datos (CORS permite null)
    V->>A: Exfiltración de API Key vía URL
    Note right of A: 🏆 Key capturada en Logs
