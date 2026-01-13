# 🔌 Secuestro de WebSocket entre sitios (CSWSH)

## 🎯 Objetivo
Establecer una conexión WebSocket no autorizada desde un dominio atacante para secuestrar la sesión de chat de la víctima y extraer sus credenciales.

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** Cross-Site WebSocket Hijacking (CSWSH) ⚓
* **Severidad:** Alta 🔴
* **Concepto clave:** Falta de validación del encabezado `Origin` y ausencia de tokens CSRF en el apretón de manos (handshake) de la conexión.

## ⚙️ Explicación Técnica
La aplicación utiliza WebSockets para un sistema de chat. Durante el proceso de actualización de HTTP a WebSocket, el servidor no verifica el origen de la petición. Aprovechando que los navegadores adjuntan automáticamente las cookies de sesión en estas peticiones, un atacante puede forzar a la víctima a abrir un canal de comunicación desde un sitio malicioso.

Una vez abierta la conexión, el script solicita el historial (`READY`) y reenvía cada mensaje entrante (que contiene las credenciales de la víctima) a un servidor externo controlado por el atacante.

## 📊 Flujo del Ataque
```mermaid
sequenceDiagram
    participant V as Navegador Víctima
    participant S as Servidor Chat (Vulnerable)
    participant A as Servidor Atacante

    V->>A: Accede a sitio malicioso
    A-->>V: Carga script de secuestro WS
    V->>S: Handshake WS (Envía Cookies de sesión)
    S-->>V: Conexión establecida (No valida Origin)
    V->>S: Envía mensaje "READY"
    S-->>V: Devuelve historial de chat (Mensajes con credenciales)
    V->>A: Exfiltra mensajes vía Fetch (Base64)
    Note right of A: 🔑 Credenciales obtenidas
