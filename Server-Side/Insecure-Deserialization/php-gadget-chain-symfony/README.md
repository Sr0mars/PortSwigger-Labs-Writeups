# 💀 Deserialización PHP con Gadget Chain (Symfony)

## 🎯 Objetivo
Lograr la **Ejecución Remota de Comandos (RCE)** en el servidor backend para eliminar el archivo `/home/carlos/morale.txt`.

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** Insecure Deserialization 🧱
* **Severidad:** Crítica 💀
* **Tecnología:** PHP / Symfony Framework
* **Vector:** Manipulación de objetos serializados firmados con una clave comprometida.

## ⚙️ Explicación Técnica
El servidor utiliza un mecanismo de serialización para gestionar tokens de sesión, protegiendo la integridad mediante una firma **HMAC SHA-1**. Tras descubrir la `Secret Key` de la aplicación, es posible falsificar objetos.

Utilizando la herramienta **PHPGGC**, se construye una cadena de gadgets basada en `Symfony/TagAwareAdapter` que, al ser deserializada, dispara una llamada a la función `exec()`.

## 📊 Flujo del Ataque
```mermaid
graph TD
    A[Atacante] -->|Descubre| B(Secret Key)
    A -->|Genera Payload| C(PHPGGC Symfony Gadget Chain)
    C -->|Firma con HMAC| D(Cookie Maliciosa)
    D -->|Inyecta| E[Servidor PHP]
    E -->|unserialize| F{Gadget Chain Execution}
    F -->|RCE| G[rm /home/carlos/morale.txt]
    G -->|Resultado| H(Laboratorio Resuelto)
