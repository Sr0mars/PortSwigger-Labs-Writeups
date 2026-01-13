Descripción: Este laboratorio presenta una configuración insegura de CORS donde la aplicación web refleja dinámicamente cualquier valor recibido en el encabezado Origin en el encabezado de respuesta Access-Control-Allow-Origin.

Vulnerabilidad identificada: La aplicación confía en cualquier origen externo y permite el envío de credenciales (Access-Control-Allow-Credentials: true). Esto permite a un atacante realizar peticiones en nombre de la víctima y leer la respuesta.

Flujo del Ataque:

La víctima visita una página maliciosa controlada por el atacante.

El script de la página maliciosa realiza una petición GET autenticada al endpoint /accountDetails.

Debido a la mala configuración de CORS, el navegador permite que el script lea la información privada (como la API Key).

El script envía (exfiltra) los datos capturados al servidor del atacante.

Impacto: Exfiltración de información sensible del perfil del usuario, incluyendo claves de API y datos personales.
