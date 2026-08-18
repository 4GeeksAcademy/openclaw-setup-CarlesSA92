# Resumen de skills activas

| # | Skill | Estado | Función principal |
| --- | --- | --- | --- |
| 1 | plan-semanal | ✅ | Plan semanal en Docs + Calendar |
| 2 | diario-aprendizaje | ✅ | Entradas de diario en Docs |
| 3 | authenticate-4geeks | ✅ | Conexión API 4Geeks |
| 4 | listar-proyectos-4geeks | ✅ | Lista proyectos con estado |
| 5 | que-me-falta-4geeks | ✅ | Proyectos pendientes |
| 6 | progreso-global-4geeks | ✅ | Visión general del curso |
| 7 | notificar-correcciones-4geeks | ✅ | Alertas Telegram |
| 8 | planificar-pendientes-4geeks | ✅ | Puente: pendientes → Calendar |

## SKILL LOG — Skills 3 a 8

*Las skills 1 y 2 fueron hechas en la anterior practica y estan reportadas en `SKILLS_DESIGN.md`*
---

## SKILL 3: authenticate-4geeks

### Prompt original
> "Cancela la busqueda. Aqui tienes la documentacion: https://github.com/4GeeksAcademy/ai-engineering-syllabus/blob/main/content/projects/openclaw-integration/STUDENT_API_CALLS_REFERENCE.es.md Para la skill de autenticacion, llamala 'authenticate-4geeks'"

### Descripción
Skill base de autenticación que provee el token de 4Geeks Academy y establece la conexión con la API de BreatheCode. Es la skill fundamental que permite a todas las demás skills autenticarse y consultar los endpoints de la API. Expone un total de **17 endpoints** para consultar perfil, cohortes, tareas, certificados, actividad, assets educativos y eventos.

### Endpoints que utiliza
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

### Resultado de prueba
```
✅ La API funciona perfectamente. 🐉
El token es válido y la conexión con 4Geeks Academy está operativa.

Tu perfil: Carles Sanchez (carles.s.a@hotmail.com) — 4Geeks Madrid
Tu cohorte principal activo: spain-aie-pt-2 (AI Engineer) — 39 días cursados, 22 micro-cohortes
Cohorte graduado: AI Engineering Introduction ✅
Tu academy_id: 6 (madrid-spain)
Tu cohort_id principal: 1672
```

---

## SKILL 4: listar-proyectos-4geeks

### Prompt original
> "Quiero crear otra Skill esta vez para Obtener mis pryectos de 4Geeks desde la API y me crees una lista con los proyectos asignados que tengo y su estado actual (pendiente, entregado, calificado)"

### Descripción
Lista todos los proyectos asignados al alumno en 4Geeks Academy con su estado actual, categorizándolos en pendientes, entregados, aprobados y rechazados. Muestra un resumen general con totales y un detalle de los proyectos pendientes con el cohorte al que pertenecen.

### Endpoints que utiliza
| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/assignment/user/me/task?task_type=PROJECT&limit=50 | Listar todos los proyectos con su estado |

### Resultado de prueba
```
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
```

---

## SKILL 5: que-me-falta-4geeks

### Prompt original
> "Quiero hacer otra Skill para acceder a la API de 4Geeks y que me digas especificamente que me falta por completar"

### Descripción
Consulta el cohorte activo del alumno y determina exactamente qué proyectos le faltan por completar para terminar el bootcamp. Se enfoca en el cohorte principal (spain-aie-pt-2), obteniendo los `pending_required_slugs` y resolviendo los nombres legibles de cada proyecto. También advierte si hay proyectos ya entregados en micro-cohortes que necesiten revisión en el cohorte principal.

### Endpoints que utiliza
| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/admissions/user/me | Obtener progreso del cohorte activo y pending_required_slugs |
| GET | /v1/assignment/user/me/task?cohort={id}&task_type=PROJECT&limit=100 | Obtener nombres legibles de proyectos pendientes |
| GET | /v1/registry/asset/{slug} | Resolver slugs a nombres de proyectos (alternativo) |

### Resultado de prueba
```
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

💪 7 proyectos para completar el bootcamp.
```

---

## SKILL 6: progreso-global-4geeks

### Prompt original
> "Crea la SKILL 6 que es un resumen global del progreso dentro del curso, no solo de los proyectos. Esta Skill muestra en porcentaje cuanto el alumno ha avanzado en el curso y cuanto le queda para completarlo, no muestra datos concretos de proyectos sino que da una vision general del avance del curso."

### Descripción
Proporciona una visión general del avance del curso mostrando porcentajes de progreso temporal (días cursados vs totales), progreso de proyectos (completados vs totales) y un progreso global ponderado. También incluye un panorama general con todos los cohortes del alumno: graduados, en curso, micro-cohortes completados y pendientes.

### Endpoints que utiliza
| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/admissions/user/me | Perfil completo con progreso de todos los cohortes |

### Resultado de prueba
```
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
```

---

## SKILL 7: notificar-correcciones-4geeks

### Prompt original
> "Si, crearemos una 7a skill que cuando un proyecto cambie de estado de 'entregado' a 'corregido' envie un mensaje de Telegram a modo de aviso para que el usuario sepa que se ha corregido ese proyecto."

### Descripción
Skill de monitorización que revisa periódicamente el estado de los proyectos del alumno en 4Geeks Academy y detecta cambios de estado, específicamente cuando un proyecto pasa de "entregado" (DONE) a "corregido" (APPROVED o REJECTED). Al detectar un cambio, envía automáticamente una notificación por Telegram. Mantiene un archivo de estado local para comparar estados anteriores con los actuales.

### Endpoints que utiliza
| Método | Endpoint | Propósito |
| --- | --- | --- |
| GET | /v1/assignment/user/me/task?task_type=PROJECT&limit=200 | Obtener todos los proyectos con estados y comparar contra archivo local |

### Formato de notificación (Telegram)
```
🐉 ¡Novedades en tus proyectos 4Geeks!

✅ APROBADO: Mi Proyecto — ¡Felicidades! 🏆

❌ RECHAZADO: Otro Proyecto — Revisa el feedback
```

### Resultado de prueba
```
✅ Skill 7 activa y funcionando. 🐉

El archivo de estado se ha inicializado con 44 proyectos:
- ✅ 30 entregados (DONE)
- ⏳ 14 pendientes (PENDING)

Ahora cuando alguno de tus proyectos sea corregido (pase a APPROVED o REJECTED),
la skill lo detectará automáticamente y te notificará por Telegram.
```

### Trigger de activación
- "Revisa si hay correcciones"
- "Hay notificaciones de proyectos"
- "Ha llegado alguna corrección?"

---

## SKILL 8: planificar-pendientes-4geeks

### Prompt original
> "Vamos a crear una 8a Skill. Esta se preguntara al usuario si quiere activarla una vez se use la SKILL 4 o 5. Esta skill preguntara al usuario si quiere crear eventos de Google Calendar para hacer los proyectos faltantes por el alumno. Si acepta, se llamara la SKILL 1 para hacer el plan semanal y que el usuario pueda añadir que proyectos quiere añadir durante la semana, en que prioridad y cuanto tiempo necesita para cada uno."

### Descripción
Skill orquestadora que actúa como puente entre las skills de consulta (skills 4 y 5) y la skill de planificación semanal (skill 1). Cuando el usuario consulta sus proyectos pendientes (mediante skill 4 o 5), esta skill pregunta al usuario si desea planificarlos en Google Calendar. Si acepta, recoge los detalles (qué proyectos, prioridad, tiempo estimado) y delega en la skill 1 (plan-semanal) para crear los eventos.

### Endpoints que utiliza
| Método | Endpoint | Propósito |
| --- | --- | --- |
| (Delega en skill 4/5) | (idem) | Obtener proyectos pendientes |
| (Delega en skill 1) | (Composio — Google Calendar) | Crear eventos calendario |

### Flujo de ejemplo
```
🐉 "He visto que tienes 7 proyectos pendientes. ¿Quieres que los planifiquemos en tu calendario?"

Tú: "Sí, los 7 con prioridad 8, 2h cada uno"

🐉 Llama a plan-semanal → busca huecos → crea eventos en Calendar ✅
```

### Resultado de prueba
```
✅ Skill 8 activada. 🐉
Ahora, cada vez que uses listar-proyectos-4geeks o que-me-falta-4geeks,
te preguntaré si quieres pasar esos proyectos pendientes al calendario.
```

