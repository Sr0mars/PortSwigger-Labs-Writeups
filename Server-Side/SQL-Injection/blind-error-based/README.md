# 💉 Blind SQL Injection (Conditional Errors)

## 🎯 Objetivo
Automatizar la extracción de la contraseña del usuario `administrator` en una base de datos **Oracle**, utilizando técnicas de inyección ciega que provocan errores controlados en el servidor.

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** Blind SQL Injection (Error-based) ⚠️
* **Severidad:** Crítica 💀
* **Base de Datos:** Oracle
* **Técnica:** Inferencia mediante errores de ejecución (División por cero).

## ⚙️ Explicación Técnica
A diferencia de la inyección condicional simple, este entorno no cambia el contenido visual de la página según la consulta. Sin embargo, al introducir una operación inválida como `1/0` (división por cero) dentro de una sentencia `CASE`, podemos forzar al servidor a devolver un **HTTP 500 Internal Server Error** solo cuando nuestra condición se cumple.

El script en Python itera sobre cada posición de la contraseña y, al recibir un código de estado 500, confirma que el carácter probado es el correcto.

## 📊 Flujo del Ataque
```mermaid
sequenceDiagram
    participant S as Script Python
    participant V as Servidor (Oracle DB)
    
    S->>V: Inyección: ¿El primer carácter es 'a'?
    V-->>S: HTTP 200 OK (Falso)
    S->>V: Inyección: ¿El primer carácter es 's'?
    Note over V: Ejecuta TO_CHAR(1/0)
    V-->>S: HTTP 500 Internal Error (Verdadero)
    Note left of S: Carácter 's' capturado
