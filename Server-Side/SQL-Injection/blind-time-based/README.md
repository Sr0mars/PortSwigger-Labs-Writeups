# 💉 Blind SQL Injection (Time-Based)

## 🎯 Objetivo
Extraer de forma sistemática la contraseña del usuario `administrator` en una base de datos **PostgreSQL**, utilizando retardos temporales para confirmar cada carácter.

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** Blind SQL Injection (Time-Based) ⏳
* **Severidad:** Crítica 💀
* **Base de Datos:** PostgreSQL
* **Técnica:** Inferencia de datos mediante la función `pg_sleep()`.

## ⚙️ Explicación Técnica
En escenarios donde el servidor no devuelve diferencias visuales ni errores ante consultas SQL inyectadas, el tiempo se convierte en el único canal de salida. Este exploit utiliza una sentencia condicional `CASE` que ejecuta `pg_sleep(3)` únicamente cuando un carácter de la contraseña coincide con nuestra prueba.

El script de Python mide la latencia de cada solicitud HTTP. Si la respuesta excede el umbral de 3 segundos, se confirma la validez del carácter y se procede a la siguiente posición.

## 📊 Flujo del Ataque
```mermaid
sequenceDiagram
    participant S as Script Python
    participant V as Servidor (PostgreSQL)
    
    S->>V: ¿Posición 1 es 'a'? (Wait 0s if false)
    V-->>S: Respuesta inmediata (200 OK)
    S->>V: ¿Posición 1 es 's'? (Wait 3s if true)
    Note over V: Ejecutando pg_sleep(3)
    V-->>S: Respuesta tras 3 segundos
    Note left of S: Carácter 's' confirmado por retardo
