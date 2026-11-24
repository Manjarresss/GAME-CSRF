# CYBER DEFENSE — OPERACIÓN CSRF (Versión 2)

**Videojuego educativo de estrategia y defensa en tiempo real**, diseñado para aprender sobre CSRF (*Cross-Site Request Forgery*). El jugador protege el servidor de un banco ficticio frente a solicitudes fraudulentas que avanzan por distintos carriles. **No es un cuestionario ni una trivia**.

## ¿Qué lo convierte en un videojuego?

- Cada petición HTTP se representa como una unidad que avanza físicamente hacia el banco.
- El jugador instala **barreras** en un tablero con cuatro carriles y tres espacios por carril.
- Cada barrera tiene un costo en créditos y un tiempo de recuperación; se puede mejorar durante la partida.
- Llegan oleadas de solicitudes fraudulentas y legítimas. Las barreras bloquean automáticamente los ataques que pueden detectar sin interrumpir las operaciones legítimas.
- Las fugas reducen la integridad y el saldo **ficticio** del banco.
- Hay recursos limitados, dificultad progresiva, cinco misiones, puntuación, estrellas y progreso local.
- Existe además un **laboratorio libre**: activar defensas, lanzar escenarios simulados y observar si el servidor acepta o rechaza la operación.

## Instrucciones para jugar

1. Abrir `index.html` en Chrome, Edge o Firefox.
2. Seleccionar **Iniciar campaña** y entrar a la misión disponible.
3. Elegir una defensa en **Arsenal defensivo**.
4. Hacer clic o tocar un nodo marcado con `+` en el carril correspondiente.
5. Pulsar **Iniciar oleada**. Las solicitudes avanzarán automáticamente hacia el servidor.
6. Usar los créditos obtenidos para instalar o mejorar defensas. Volver a pulsar un nodo ocupado lo mejora por 45 créditos.
7. Evitar que la integridad llegue a cero. Completar la misión desbloquea la siguiente.

**Controles:** ratón, touch o teclado (1–5 elige una herramienta, espacio inicia/pausa, P pausa). El sonido es opcional. En móviles hay una barra de herramientas accesible justo encima del tablero.

## Misiones

| Nivel | Título | Aprendizaje técnico |
| --- | --- | --- |
| 1 | La sesión comprometida | Cookies de sesión y ataques CSRF clásicos |
| 2 | Puertas de acceso | Login CSRF y validación en formularios de autenticación |
| 3 | La trampa del GET | SameSite=Lax, solicitudes GET inseguras, limitaciones de la protección |
| 4 | JavaScript engañado | Client-side CSRF y validación de destinos y rutas |
| 5 | Asedio final | Defensa en profundidad y respuesta a múltiples ataques |

## Defensas y reglas representadas

- **TOKEN CSRF:** verifica un token impredecible asociado a la sesión. En el modelo frena CSRF clásico y Login CSRF en POST. No detiene Client-side CSRF cuando el JavaScript legítimo adjunta un token válido.
- **ORIGIN GATE:** validación de cabeceras de origen para rechazar POST desde orígenes no autorizados. No bloquea solicitudes generadas por JavaScript del origen legítimo.
- **SameSite=Lax (global):** reduce la exposición de cookies en solicitudes POST entre sitios; no sustituye a los tokens. No resuelve por sí solo Login CSRF ni operaciones GET inseguras.
- **GET SEGURO:** modifica el diseño de una ruta para que las peticiones GET no cambien datos.
- **VALIDAR DATOS:** valida destinos, rutas y operaciones aceptadas; detiene manipulaciones del lado del cliente.
- **REAUTENTICAR:** añade un control adicional en operaciones sensibles, como cambios de cuenta o transferencia.

**Nota didáctica:** los controles de seguridad no son magia ni equivalen exactamente a cómo se aplican todos los frameworks o navegadores. Este videojuego abstrae detalles para permitir comprender *qué protege cada mecanismo* y *qué amenazas no cubre*. SameSite es un atributo de cookies del navegador; los tokens y las validaciones se aplican en el servidor. Las operaciones GET no deberían modificar estado. En el juego se representa únicamente el comportamiento conceptual esperado.

## Estructura

```text
CyberDefense_CSRF_V2/
├── index.html            # Interfaz, pantallas, carriles y laboratorio
├── styles.css            # Diseño adaptable (desktop, tablet, móvil)
├── game.js               # Motor de juego, reglas y simulaciones
├── assets/
│   └── favicon.svg       # Ícono vectorial
├── docs/
│   ├── inicio_escritorio.png
│   ├── defensa_colocada.png
│   ├── oleada_en_curso.png
│   ├── laboratorio.png
│   └── inicio_movil.png
├── GUIA_PARA_EXPONER.md
└── README.md
```

## Cómo ejecutarlo

**No necesita instalaciones ni servidor.** Descomprimir la carpeta y abrir `index.html` directamente con un navegador. Si lo prefieres, VS Code + Live Server también funciona, pero no es necesario. No usa PHP, XAMPP, MySQL ni servicios externos para la lógica. Las fuentes web son opcionales; si no se cargan, se utilizan las alternativas del sistema.

## Publicarlo gratis

### Netlify Drop (recomendado)
1. Abrir `https://app.netlify.com/drop`.
2. Arrastrar la carpeta que contiene `index.html` o cargar el ZIP de publicación que se entrega por separado.
3. Netlify generará una URL pública de la forma `https://nombre-del-sitio.netlify.app`.
4. Abrir la URL desde otro dispositivo, verificar que cargue el juego y copiarla como enlace de entrega.

La URL pública **no puede generarse sin publicar el proyecto en una cuenta de hosting**. El archivo ya está listo para esa operación.

### GitHub Pages / Cloudflare Pages
Son alternativas compatibles con sitios web estáticos. Publicar el contenido de la carpeta raíz; no se requiere comando de build.

## Uso de inteligencia artificial generativa (requisito de la actividad)

**Herramienta:** ChatGPT (OpenAI).

**Aportes:** ideación de mecánicas y progresión de cinco niveles, diseño de interfaz, creación del código HTML/CSS/JavaScript, modelado didáctico de los ataques y protecciones, redacción de contenidos y README, y apoyo en pruebas del flujo con un navegador automatizado.

**Revisión humana:** quien entrega el proyecto debe jugarlo y evaluar si la explicación técnica, los ejemplos, el diseño y la dificultad son apropiados para la asignatura, así como verificar el enlace después de publicarlo.

## Protección y ética

Todo el juego funciona con un banco y solicitudes simulados **dentro del navegador**. No intenta atacar servidores reales, no roba sesiones ni credenciales, no hay cuentas reales, no solicita datos personales y no envía resultados a servidores externos. El progreso se guarda mediante `localStorage` en el navegador del jugador, cuando está disponible.

## Comprobaciones realizadas

- Se completó la primera misión en navegador automatizado con 100 % de integridad.
- Se probó la misión final con seis barreras instaladas y dos mejoras: se completó y se registraron 34 solicitudes maliciosas bloqueadas.
- Se ensayaron los cuatro ataques del laboratorio libre y sus mitigaciones correspondientes.
- Se verificó que las vistas del juego no causen desbordamiento horizontal a 390 px.
- Se verificó la sintaxis JavaScript y la ausencia de errores de ejecución durante las pruebas anteriores.

**Pendiente:** publicación en una cuenta de hosting gratuita y comprobación del enlace público por parte del usuario.
