# 🎭 XSS to CSRF: Evasión de protecciones mediante encadenamiento

## 🎯 Objetivo
Comprometer la cuenta de un usuario cambiando su correo electrónico de forma automática y silenciosa, utilizando una vulnerabilidad de **XSS almacenado** para anular la protección **CSRF**.

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** Stored XSS + CSRF Bypass 🧬
* **Severidad:** Crítica 💀
* **Vector:** Comentarios del blog (XSS Almacenado).

## ⚙️ Explicación Técnica
Aunque la aplicación utiliza tokens CSRF para proteger acciones sensibles, un atacante con capacidad de ejecutar JavaScript en el contexto del usuario (XSS) puede leer el DOM de la página.

El exploit realiza los siguientes pasos de forma automática:
1. **Fetch:** El navegador de la víctima solicita la página `/my-account`.
2. **Parsing:** El script localiza y extrae el valor del token CSRF del formulario.
3. **Execution:** Se realiza una petición `POST` al endpoint de cambio de correo incluyendo el token legítimo extraído, validando así la petición ante el servidor.

## 📊 Flujo del Ataque
```mermaid
sequenceDiagram
    participant V as Víctima (Navegador)
    participant S as Servidor Web
    
    V->>S: Lee comentario con XSS malicioso
    V->>S: GET /my-account (Petición automática oculta)
    S-->>V: HTML con Token CSRF legítimo
    Note over V: Script extrae el Token del HTML
    V->>S: POST /change-email (Email malicioso + Token robado)
    S-->>V: 200 OK - Email Cambiado
    Note right of S: 🚩 Cuenta comprometida
