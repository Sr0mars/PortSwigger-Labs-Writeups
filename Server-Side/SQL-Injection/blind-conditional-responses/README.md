# 💉 Blind SQL Injection con Respuestas Condicionales

## 🎯 Objetivo
Extraer la contraseña del usuario `administrator` mediante una técnica de **Blind SQLi** booleana, automatizando el proceso con un script de Python.

## 🛡️ Detalles de la Vulnerabilidad
* **Vulnerabilidad:** Blind SQL Injection (Conditional Responses) 🕳️
* **Severidad:** Crítica 💀
* **Técnica:** Inferencia de datos carácter a carácter mediante lógica booleana.

## ⚙️ Explicación Técnica
La aplicación es vulnerable a SQLi a través de la cookie `TrackingId`. Al inyectar una subconsulta que devuelve un valor verdadero (TRUE), la página muestra un mensaje de bienvenida ("Welcome back"). Si la consulta es falsa, el mensaje desaparece.

El script de Python automatiza este proceso:
1. Utiliza la función `SUBSTRING()` para aislar un carácter de la contraseña en una posición específica.
2. Compara ese carácter con un set predefinido (letras y números).
3. Analiza la respuesta HTTP para confirmar si el carácter es correcto.

## 📊 Flujo del Ataque
```mermaid
graph TD
    A[Inicio Script Python] --> B{¿Posición 1 a 20?}
    B -->|Sí| C[Probar Carácter 'a', 'b', 'c'...]
    C --> D[Enviar Petición con Inyección]
    D --> E{¿Respuesta contiene 'Welcome back'?}
    E -->|No| C
    E -->|Sí| F[Guardar Carácter y pasar a Posición +1]
    F --> B
    B -->|No| G[🏆 Password Completa Obtenida]
