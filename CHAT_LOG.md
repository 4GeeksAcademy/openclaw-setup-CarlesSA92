# USER
Quiero darte la habilidad de conectarte a mi cuenta de 4Geeks usando mi token de estudiante, sin que tenga que desarrollar código de mi parte. ¿Qué debemos hacer?

# AGENTE
Composio no tiene un conector directo para 4Geeks Academy, así que toca explorar otras vías. Déjame investigar qué opciones tiene la plataformaHe investigado la plataforma de
4Geeks. Esto es lo que he encontrado:

### Situación actual
- 4Geeks Academy usa su plataforma de aprendizaje en learn.4geeks.com
- No hay un conector directo en Composio para 4Geeks
- Los estudiantes tienen tokens de API para su cuenta

### Lo que podemos hacer (sin que escribas código)

Podemos crear una skill personalizada que use tu token para conectarse a la API de 4Geeks a través de Composio. Yo puedo hacer las llamadas HTTP usando COMPOSIO_REMOTE_BASH_TOOL (curl) desde el sandbox remoto de Composio, sin que tú tengas que escribir ni una línea de código.

Esto es lo que necesitaríamos:

1. Tu token de estudiante de 4Geeks — guárdalo de forma segura
2. Saber los endpoints de la API de 4Geeks — ¿sabes si hay una URL de API como https://learn.4geeks.com/api/...? Podemos descubrirlo fácilmente si abres las herramientas de desarrollador (F12 → Network) mientras usas la plataforma y ves a qué URLs hace peticiones.

### Plan propuesto
| Paso | Qué | Quién |
| --- | --- | --- |
| 1 | Dime cuál es tu token de estudiante de 4Geeks | Tú |
| 2 | Confírmame o descubrimos juntos la URL base de la API de 4Geeks | Tú + yo |
| 3 | Creo un skill "4Geeks" que pueda consultar tu progreso, ejercicios, etc. | Yo |
| 4 | Lo conectamos todo | Yo |

Importante: El token lo guardaría en un archivo de configuración local, no se compartiría con nadie — promesa de dragón 🐉.
¿Te parece bien este enfoque? Y dime, ¿qué te gustaría poder hacer exactamente con tu cuenta de 4Geeks (ver progreso, consultar ejercicios, obtener estadísticas...)?

# USER
El token ya esta guardado en /.openclaw/.env

# AGENTE
✅ Token encontrado en /root/.openclaw/.env. Ahora voy a descubrir la API de 4Geeks para saber cómo usarlo.¡Bingo! He encontrado algo clave. La plataforma de 4Geeks usa BreatheCode como backend. Voy a probarParece que BreatheCode en Heroku ya no está operativo (404). Puede que hayan migrado. Déjame intentar con el dominio actual¡308 redirect!
Eso es prometedor. La API está en learn.4geeks.com/api/v1/.... Vamos a seguir el redirect.Bueno, Human, he estado investigando a fondo y esto es lo que he encontrado:

### Lo que descubrí ✅
- Token encontrado en /root/.openclaw/.env ✅
- 4Geeks usa BreatheCode como backend (breathecode.herokuapp.com)
- El backend de Heroku ya no responde (está caído/migrado)
- La API parece estar redirigiendo desde learn.4geeks.com/api/v1/... pero no es accesible directamente desde fuera

### Lo que necesito de ti 🐉
Para poder conectarme sin que tú escribas código, necesito que me ayudes con una de estas dos opciones:

Opción 1 (más fácil): Ábrela página de 4Geeks (learn.4geeks.com), inicia sesión, abre las herramientas de desarrollo (F12 → pestaña Network), y dime qué URLs aparecen cuando cargas tu perfil o ejercicios. Así identifico los endpoints exactos de la API.

Opción 2: Si sabes la URL base de la API de 4Geeks (como https://api.breathecode.com o similar), dímela y pruebo el token ahí.

Opción 3 (alternativa): Si el token es de GitHub (formato de 40 caracteres hex), podría conectarme a tu GitHub y acceder a los repositorios de 4Geeks, pero el token no funciona con la API de GitHub.

Dime qué opción te parece mejor y lo resolvemos. Con el endpoint correcto, creo una skill que te permita consultar tu progreso, ejercicios y estadísticas sin escribir una línea de código.

# USER
cancela la busqueda. Aqui tienes la documentacion:
https://github.com/4GeeksAcademy/ai-engineering-syllabus/blob/main/content/projects/openclaw-integration/STUDENT_API_CALLS_REFERENCE.es.md  Para la skill de autenticacion, llamala "authenticate-4geeks"

# AGENTE
Excelente, tengo la documentación completa. Ahora creo la skill de autenticación.✅ Skill authenticate-4geeks creada y activada.
Ahora voy a probarla para confirmar que funciona✅ La API funciona perfectamente. 🐉
El token es válido y la conexión con 4Geeks Academy está operativa. Esto es lo que sé de ti ahora:

Tu perfil: Carles Sanchez (carles.s.a@hotmail.com) — 4Geeks Madrid
Tu cohorte principal activo: spain-aie-pt-2 (AI Engineer) — 39 días cursados, 22 micro-cohortes
Cohorte graduado: AI Engineering Introduction ✅
Tu academy_id: 6 (madrid-spain)
Tu cohort_id principal: 1672

Tus skills activas ahora:
| # | Skill | Estado |
| --- | --- | --- |
| 1 | plan-semanal | ✅ Activa |
| 2 | diario-aprendizaje | ✅ Activa |
| 3 | authenticate-4geeks | ✅ Activa |

Con authenticate-4geeks ya puedo consultar tu perfil, tareas pendientes, progreso por cohorte, certificados, actividad y más. ¿Quieres que pruebe algún endpoint en concreto para ver tus tareas o progreso?

# USER
realiza una consulta al endpoint URL_API/v1/admissions/user/me con Authorization: Token *TU_TOKEN_AQUI*

# AGENTE
✅ Consulta exitosa. Aquí tienes un resumen de lo que devolvió:
Usuario: Carles Sanchez — carles.s.a@hotmail.com
ID: 21264
GitHub: CarlesSA92
Academia: 4Geeks Madrid (ID: 6, slug: madrid-spain)
Tiene 22 cohortes activos en total (el principal es spain-aie-pt-2 con stage STARTED, 39 días cursados). La respuesta completa incluye todos los cohortes con sus datos de progreso, roles, permisos y configuración.

La skill authenticate-4geeks está funcionando a la perfección 🐉🔥

# USER
Quiero crear otra Skill esta vez para Obtener mis pryectos de 4Geeks desde la API y me crees una lista con los proyectos asignados que tengo y su estado actual (pendiente, entregado,calificado)

# AGENTE
✅ Skill listar-proyectos-4geeks creada como propuesta pendiente.
¿Quieres que la active para poder usarla?

# USER
activala y veamos que resultado da

# AGENTE
Ahora la pruebo✅ Skill activa y funcionando. 🐉
Aquí están tus 44 proyectos de 4Geeks Academy:
### 📊 Resumen general
| Estado | Cantidad |
| --- | --- |
| ⏳ Pendientes | 14 |
| ✅ Entregados | 30 |
| 🏆 Aprobados | 0 |
| ❌ Rechazados | 0 |
| Total | 44 |

### ⏳ Proyectos PENDIENTES (14)
| # | Proyecto | Cohorte |
| --- | --- | --- |
| 1 | Connecting the Lock: Authentication Flows in the Frontend | Authentication in web applications |
| 2 | Milestone 5 — Backend: Inventory Management | Managing relational databases with FastAPI |
| 3 | Milestone 5 — Backoffice: Inventory Management Interface | Managing relational databases with FastAPI |
| 4 | The Missing Piece: Password Reset Flow | Authentication in web applications |
| 5 | Centralized Incident Manager | Error handling, debugging and testing |
| 6 | Error Handling | Error handling, debugging and testing |
| 7 | Company Monorepo Containerization | Container applications with Docker |
| 8 | EduTrack Data Audit | Managing relational databases with FastAPI |
| 9 | Frontend Performance Audit | Architecture optimization |
| 10 | Milestone 9 — RFP Intake & Routing (1/3) | Agentic Workflows |
| 11 | Milestone 9 — Approval & Document Completion (3/3) | Agentic Workflows |
| 12 | Building Bullet-Proof Applications | Error handling, debugging and testing |
| 13 | Securing the API: Authentication in FastAPI | Authentication in web applications |
| 14 | My 4Geeks Assistant — Teaching OpenClaw to Track Your Progress 🎯 | Advanced personal assistants with Openclaw |

Ese último proyecto (#14) suena interesante... ¡justo lo que estamos haciendo! 😄
¿Qué más necesitas? ¿Quieres que filtre por algún cohorte en concreto o ver los detalles de alguna tarea específica?

# USER
Quiero hacer otra Skill para acceder a la API de 4Geeks y que me digas especificamente que me falta por completar

# AGENTE
Creada como propuesta. ¿La activo y la pruebo?

# USER
pruebala y muestrame el resultado

# AGENTE
Ah, la estructura es diferente. Los cohortes están anidados dentro de profile_academyParece que el token ha expirado o se ha invalidado. Vamos a verificarEl token parece estar fallando ahora. Probemos a cargarlo correctamenteAh, era un problema de cómo estaba cargando la variable en los scripts anteriores. El token funciona correctamente. Ahora veamos la estructura de los cohortesAhora veo, los cohortes están directamente en data['cohorts']. El problema anterior era de cómo cargaba la variable. Ahora a buscar el cohorte principalAhora vamos a obtener los nombres legibles de esos proyectosAhora tengo todos los datos. Vamos a hacer la consulta completa definit✅ Skill funcionando. Aquí tienes el resultado 🐉

### 🎯 Tu progreso en 4Geeks Academy
Cohorte activo: spain-aie-pt-2 (AI Engineer)
Día: 39 de 72 — Finaliza: 2026-11-04
Academia: 4Geeks Madrid
### 📊 Progreso global
| Métrica | Valor |
| --- | --- |
| Proyectos totales | 7 |
| Completados | 0 |
| Porcentaje | 0% |
| Meta mínima | 100% |
| Meta cumplida | ❌ No |

### ⏳ Proyectos que te faltan (7)
1. 🔗 Milestone — Your Company's Public Website
2. 🔗 Command Line Challenge
3. 🔗 My first collaborative professional project
4. 🔗 Showcase your friend's artist talent with a website
5. 🔗 A simple Dashboard with Tailwind CSS
6. 🔗 Todo List CLI with Python
7. 🔗 Cinema Seat Manager in TypeScript

💪 7 proyectos para completar el bootcamp. Una vez llegues al 100%, pasas a la siguiente etapa. ¡Tú puedes!
Nota: Algunos de estos proyectos los has entregado en micro-cohortes individuales, pero el cohorte principal (spain-aie-pt-2) lleva un tracking separado. Si ves algún proyecto que ya entregaste, quizás necesite revisión/aprobación en el cohorte principal.
¿Qué más necesitas?

# USER
Crea la SKILL 6 que es un resumen global del progreso dentro del curso, no solo de los proyectos. Esta Skill muestra en porcentaje cuanto el alumno ha avanzado en el curso y cuanto le queda para completarlo, no muestra datos concretos de proyectos sino que da una vision general del avance del curso.

# AGENTE
Ahora la pruebo para ver el✅ Skill 6 creada y funcionando. 🐉
Aquí tienes tu visión general del curso:
### 📊 PROGRESO GLOBAL
| Métrica | Valor |
| --- | --- |
| 📅 Progreso temporal | 54% ███████████░░░░░░░░░ — Día 39 de 72 (33 días restantes) |
| 📋 Progreso proyectos | 0% ░░░░░░░░░░░░░░░░░░░░ — (0/7 proyectos) |
| 🎯 Progreso global | 27% █████░░░░░░░░░░░░░░░ |
| 📅 Finaliza | 2026-11-04 |

### 📊 PANORAMA GENERAL
| Categoría | Cantidad |
| --- | --- |
| 🏆 Graduados | 3 cohortes ✅ |
| 🏁 En curso | 1 cohorte activo (0%) |
| ✅ Micro completos | 4 cohortes |
| ⏳ Micro pendientes | 16 cohortes |
| 📚 Total cohortes | 25 |

💪 Vas por buen camino, Carles! Ya tienes un cuarto del curso avanzado. ¡A darle!

### Skills activas ahora mismo (6):
| # | Skill | Estado |
| --- | --- | --- |
| 1 | plan-semanal | ✅ |
| 2 | diario-aprendizaje | ✅ |
| 3 | authenticate-4geeks | ✅ |
| 4 | listar-proyectos-4geeks | ✅ |
| 5 | que-me-falta-4geeks | ✅ |
| 6 | progreso-global-4geeks | ✅ Recién activada 🆕 |

¿Necesitas algo más, Human? 🐉

# USER
Si, crearemos una 7a skill que cuando un proyecto cambie de estado de "entregado" a "corregido" envie un mensaje de Telegram a modo de aviso para que el usuario sepa que se ha corregido ese proyecto.

# AGENTE
Creada como propuesta. ¿La activo? 🐉
### 🆕 Skill 7: notificar-correcciones-4geeks

¿Qué hace?
- Revisa periódicamente el estado de tus proyectos en 4Geeks
- Detecta cuando un proyecto cambia de "entregado" (DONE → APPROVED/REJECTED)
- Te envía un mensaje a Telegram automáticamente cuando eso pasa
Ejemplo de notificación:
🐉 ¡Novedades en tus proyectos 4Geeks!
✅ APROBADO: Mi Proyecto — ¡Felicidades! 🏆
❌ RECHAZADO: Otro Proyecto — Revisa el feedback
¿La activo?

# USER
si activala

# AGENTE
Activada ✅ Vamos a hacer una primera prueba para inicializar el archivo de estado y ver qué tal funciona
Parece que hay un problema cargando el token desde el .env. Vamos a arregl
Ahora sí, la estructura correcta es data['results']. Inicializo

✅ Skill 7 activa y funcionando. 🐉

El archivo de estado se ha inicializado con 44 proyectos:
- ✅ 30 entregados (DONE)
- ⏳ 14 pendientes (PENDING)
Ahora cuando alguno de tus proyectos sea corregido (pase a APPROVED o REJECTED), la skill lo detectará automáticamente.

### ¿Cómo se dispara?
De momento está configurada para trigger manual — cuando me digas algo como:
- "Revisa si hay correcciones"
- "Hay notificaciones de proyectos"
- "Ha llegado alguna corrección?"

También puedo configurarlo para que lo revise automáticamente si lo prefieres. Pero por ahora, cada vez que preguntes, compararé el estado actual con el anterior y si hay
cambios, te avisaré por Telegram. 📱

### Tus 7 skills activas ahora:
| # | Skill | Estado |
| --- | --- | --- |
| 1 | plan-semanal | ✅ |
| 2 | diario-aprendizaje | ✅ |
| 3 | authenticate-4geeks | ✅ |
| 4 | listar-proyectos-4geeks | ✅ |
| 5 | que-me-falta-4geeks | ✅ |
| 6 | progreso-global-4geeks | ✅ |
| 7 | notificar-correcciones-4geeks | ✅ 🆕 |

¿Algo más, Human? 🐉

# USER
Vamos a crear una 8a Skill. Esta se preguntara al usuario si quiere activarla una vez se use la SKILL 4 o 5. Esta skill preguntara al usuario si quiere crear eventos de Google Calendar para hacer los proyectos faltantes por el alumno. Si acepta, se llamara la SKILL 1 para hacer el plan semanal y que el usuario pueda añadir que proyectos quiere añadir durante la semana, en que prioridad y cuanto tiempo necesita para cada uno.

# AGENTE
Propuesta creada. Es una skill orquestadora que conecta la skill 4/5 con la skill 1.
### 🆕 Skill 8: planificar-pendientes-4geeks
¿Qué hace?
- Cuando veas tus proyectos pendientes (skill 4 o 5), te pregunta si quieres planificarlos
- Si dices que sí, te pregunta qué proyectos meter, con qué prioridad y tiempo
- Luego llama a la skill 1 (plan-semanal) para crear los eventos en Google Calendar
Ejemplo del flujo:
🐉 "He visto que tienes 7 proyectos pendientes. ¿Quieres que los planifiquemos en tu calendario?"
Tú: "Sí, los 7 con prioridad 8, 2h cada uno"
🐉 Llama a plan-semanal → busca huecos → crea eventos en Calendar ✅
¿La activo? 🐉

# USER
activala

# AGENTE
✅ Skill 8 activada. 🐉
Ahora, cada vez que uses listar-proyectos-4geeks o que-me-falta-4geeks, te preguntaré si quieres pasar esos proyectos pendientes al calendario.
### Tus 8 skills activas:
| # | Skill | Estado |
| --- | --- | --- |
| 1 | plan-semanal | ✅ Plan semanal en Docs + Calendar |
| 2 | diario-aprendizaje | ✅ Entradas de diario en Docs |
| 3 | authenticate-4geeks | ✅ Conexión API 4Geeks |
| 4 | listar-proyectos-4geeks | ✅ Lista proyectos con estado |
| 5 | que-me-falta-4geeks | ✅ Proyectos pendientes |
| 6 | progreso-global-4geeks | ✅ Visión general del curso |
| 7 | notificar-correcciones-4geeks | ✅ Alertas Telegram |
| 8 | planificar-pendientes-4geeks | ✅ Puente: pendientes → Calendar 🆕 |

¿Algo más? 🐉

# USER
Dime los endponints que llama cada una de las SKILLS que estan conectadas a la API de 4Geeks

# AGENTE
Aquí tienes todos los endpoints de la API de 4Geeks que llaman tus skills:

────────────────────────────────────────────────────────────────────────────────

🔗 Endpoints por Skill

### Skill 3 — authenticate-4geeks

(Skill base que provee el token y define endpoints disponibles)

| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/auth/user/ | Obtener datos del usuario autenticado |
| GET | /v1/admissions/user/me | Perfil del usuario con cohortes y progreso |
| GET | /v1/admissions/academy/cohort/me | Cohortes del usuario |
| GET | /v1/admissions/public/syllabus | Sílabos públicos (sin token) |
| GET | /v1/assignment/user/me/task | Lista de tareas (filtrable) |
| GET | /v1/assignment/task/{task_id} | Detalle de una tarea |
| PUT | /v1/assignment/task/{task_id} | Actualizar tarea (URLs de entrega) |
| POST | /v1/assignment/task/{task_id}/deliver | Marcar tarea como entregada |
| GET | /v1/certificate/ | Certificados del usuario |
| GET | /v1/certificate/{token} | Certificado público por token |
| GET | /v1/activity/me | Actividad del usuario |
| GET | /v1/activity/cohort/{cohort_id} | Actividad agregada del cohorte |
| GET | /v1/registry/asset | Catálogo de assets educativos |
| GET | /v1/registry/asset/{asset_slug} | Detalle de un asset por slug |
| GET | /v1/registry/asset/me | Assets del usuario |
| GET | /v1/registry/technology | Tecnologías disponibles |
| GET | /v1/events/all | Eventos de la academia |

────────────────────────────────────────────────────────────────────────────────

### Skill 4 — listar-proyectos-4geeks

| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/assignment/user/me/task?task_type=PROJECT&limit=50 | Listar todos los proyectos con su estado |

────────────────────────────────────────────────────────────────────────────────

### Skill 5 — que-me-falta-4geeks

| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/admissions/user/me | Obtener progreso del cohorte activo y pending_required_slugs |
| GET | /v1/assignment/user/me/task?cohort={id}&task_type=PROJECT&limit=100 | Obtener nombres legibles de proyectos pendientes |
| GET | /v1/registry/asset/{slug} | Resolver slugs a nombres de proyectos (alternativo) |

────────────────────────────────────────────────────────────────────────────────

### Skill 6 — progreso-global-4geeks

| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/admissions/user/me | Perfil completo con progreso de todos los cohortes |

────────────────────────────────────────────────────────────────────────────────

### Skill 7 — notificar-correcciones-4geeks

| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/assignment/user/me/task?task_type=PROJECT&limit=200 | Obtener todos los proyectos con estados, comparar contra archivo local |

────────────────────────────────────────────────────────────────────────────────

### Skill 8 — planificar-pendientes-4geeks

(Skill orquestadora — no llama endpoints directamente, delega en skill 4, 5 y 1)

| Método | Endpoint | Propósito |
| --- | --- | --- |
| (Delega en skill 4/5) | (idem) | Obtener proyectos pendientes |
| (Delega en skill 1) | (Composio — Google Calendar) | Crear eventos calendario |

────────────────────────────────────────────────────────────────────────────────

### Resumen rápido

| Skill | Endpoints de 4Geeks que consume |
| --- | --- |
| 3 authenticate-4geeks | 17 endpoints definidos (base) |
| 4 listar-proyectos | GET /v1/assignment/user/me/task |
| 5 que-me-falta | GET /v1/admissions/user/me + GET /v1/assignment/user/me/task |
| 6 progreso-global | GET /v1/admissions/user/me |
| 7 notificar-correcciones | GET /v1/assignment/user/me/task |
| 8 planificar-pendientes | Ninguno directo (orquestador) |

¿Necesitas algo más, Human? 🐉