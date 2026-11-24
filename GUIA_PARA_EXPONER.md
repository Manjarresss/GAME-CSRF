# GUÍA DE DEMOSTRACIÓN — CYBER DEFENSE CSRF

## Introducción breve (30 segundos)

«Nuestra vulnerabilidad asignada fue CSRF, que ocurre cuando un atacante consigue que el navegador de una persona autenticada intente realizar operaciones que esa persona no autorizó. Para mostrarlo, desarrollamos un videojuego de defensa en tiempo real. No es una trivia: aquí se construye la seguridad del sistema, se enfrentan oleadas de solicitudes y se observa el efecto de cada medida preventiva».

## Demostración del videojuego (2 a 3 minutos)

1. Abre el juego, selecciona **Iniciar campaña** y entra a la primera misión.
2. Señala los dos carriles activos: transferencia y perfil. Cada círculo representa una petición HTTP que se dirige hacia el servidor de CyberBank.
3. Selecciona **TOKEN CSRF** y colócalo en un nodo vacío de cada carril. Aclara que no es un token inventado por el usuario: en una aplicación real el servidor lo genera y valida.
4. Presiona **Iniciar oleada** y muestra cómo se mueven las solicitudes. Las maliciosas quedan detenidas y las legítimas atraviesan la red para llegar al banco.
5. Observa la integridad, los ataques bloqueados y los créditos. Completa la misión y muestra la pantalla de resultados y el aprendizaje técnico.
6. Si tienes tiempo, abre la tercera misión para explicar que SameSite=Lax no arregla un endpoint GET inseguro, o la cuarta para explicar por qué Client-side CSRF puede incluir un token válido.

## Demostración del laboratorio libre (1 a 2 minutos)

1. Regresa al inicio y abre **Laboratorio libre**.
2. Deja todas las defensas desactivadas y lanza «POST malicioso desde otra web». El saldo ficticio baja: la simulación representa un servidor vulnerable que procesa la solicitud.
3. Activa **Token anti-CSRF**, **Origin** o **SameSite=Lax** y repite la prueba. La solicitud se rechaza; el saldo permanece igual.
4. Elige «Client-side CSRF». Muestra que el token y SameSite no bastan por sí solos en ese ejemplo. Activa **Validación de entradas** y repite.
5. Concluye que se requieren controles en distintas capas de la aplicación.

## Cierre breve (20 segundos)

«A través del juego demostramos que una sesión válida no garantiza que una operación sea legítima. Aprendimos a elegir controles defensivos y también a reconocer sus limitaciones. El proyecto se desarrolló con HTML, CSS y JavaScript y utilizamos ChatGPT como apoyo para diseño, contenidos y programación».

## Evidencias sugeridas

- Captura del inicio del videojuego.
- Captura de una partida con solicitudes moviéndose por los carriles.
- Captura del arsenal instalado y la integridad del banco.
- Captura del laboratorio libre antes y después de activar una defensa.
- Enlace público del sitio tras publicarlo en Netlify.
- Código fuente (`index.html`, `styles.css`, `game.js`) y README con el aporte de IA.

## Advertencias para explicar con precisión

- Es una simulación educativa local; no se está atacando un banco real.
- SameSite=Lax se aplica al envío de cookies por el navegador; no garantiza prevenir todos los CSRF.
- Login CSRF no depende necesariamente de una cookie de sesión previa.
- Las aplicaciones seguras no deberían permitir cambios de estado mediante GET.
- No confundas Client-side CSRF con el CSRF clásico; el primero puede originarse a través de JavaScript legítimo.
