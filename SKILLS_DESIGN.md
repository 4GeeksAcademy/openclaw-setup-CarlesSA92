# SKILL 1: Plan semanal
**¿Qué hace esta skill?**
Formatea un listado de objetivos y compromisos y el agente lo escribe como un plan semanal prioridad, guardandolo en un documento de Google Docs estructurado y crea los eventos clave en Google Calendar.

**¿Qué input necesita el agente?**
El usuario debe decirle al agente que quiere "planificar la semana". A continuación debera listar una serie de tareas que deben tener los siguientes parametros:
- Nombre de la actividad (obligatorio): descriptivo de lo que hay que hacer
- Prioridad (obligatorio): del 0 al 10 que tan urgente es
- Tiempo reservado para esa actividad (obligatorio): en horas especificar el aproximado de cuanto tiempo se puede necesitar para completarlo
- Descripción extra de la tarea (opcional): cualquier punto extra que deba quedar reflejado como recordatorio.

En caso de faltar un campo obligatorio, el agente preguntará al usuario por dicho campo antes de continuar.

**¿Cómo es un buen output?**
Cuando el usuario menciona "planificar la semana" el agente pedira al usuario la información de la primera tarea:
"Por favor, dime el plan de tareas:
- Nombre de la actividad (obligatorio): descriptivo de lo que hay que hacer
- Prioridad (obligatorio): del 0 al 10 que tan urgente es
- Tiempo reservado para esa actividad (obligatorio): en horas especificar el aproximado de cuanto tiempo se puede necesitar para completarlo
- Descripción extra de la tarea (opcional): cualquier punto extra que deba quedar reflejado como recordatorio." 

El usuario responderá a cada campo con la información requerida. Por ejemplo:
"- *Nombre de la actividad:* Estudiar Ingineria de IA en 4Geeks
- *Prioridad:* 8
- *Tiempo reservado para esa actividad:* 2 horas
- *Descripción extra de la tarea:* Estudiar modelos de agentes y creacion de skills"

O otro ejemplo:
"Tengo que Estudiar Ingenieria de IA en 4Geeks durante 2 horas, consideralo una prioridad de rango 8. El temario a estudiar es sobre los modelos de agentes y creacion de skills"

El agente revisará los campos introducidos y si falta algun campo obligatorio, avisara al usuario de que dicho campo esta vacio y que el usuario debe dar información al respecto. 

Una vez la tarea esta completa, el agente revisará el calendario y buscará el primer hueco disponible que tenga suficiente tiempo para añadir la tarea. No debe solaparse con otras y a ser possible deberia dejar unos 30 minutos entre tarea y tarea de descanso. Una vez encontrado un espacio, le informará al usuario de la franja horaria a reservar esperando confirmación del usuario. 

Una vez confirmada la franja horaria, el agente procederá a crear el evento en Google Calendar. A continuación informará al usuario de que dicho evento para la tarea ha sido creado con exito o si ha habido algun problema.

Si la tarea solapa con otra o no hay suficiente margen entre ellas, el agente informará al usuario al respecto. 

Si ha habido algun error durante la creación de la tarea o la introducción de los campos, el agente informará del problema al usuario para que pueda ser revisado y solucionado en la menor brevedad posible.

# SKILL 2: Diario de aprendizaje
**¿Qué hace esta skill?**
A partir de una lista de puntos que el usuario le da al agente, este lo formatea y crea una entrada estructurada en un documento de Google Docs con fecha y texto para llevar un control de lo que se ha hecho durante el dia.
**¿Qué input necesita el agente?**
Decir al agente "crear entrada para el diario", "diaro personal" o "entrada diario".
A continuación el agente informará al usuario que esta listo para tomar apuntes sobre la nueva entrada y el usuario redactará los puntos a introducir.

**¿Cómo es un buen output?**
Con una entrada del usuario parecida a la siguiente:
"- Completado proyecto 4Geeks sobre las skills del agente
- Estudiado 4 temas del temario
- Ejercicio durante 1 hora"

El agente tomará nota y buscará el documento de Google Docs con nombre "Diario del usuario", en caso de no existir, lo creará. 

El agente buscará la ultima página escrita y **sin eliminar contenido**, hará un salto de pagina para escribir la siguiente entrada. Por ejemplo:

"**Fecha 18/08/2026:**
El usuario hoy ha sido productivo y ha completado un proyecto de sus estudios en 4Geeks relacionado con las skills de los agentes IA a parte de estudiar 4 temarios de la academia. Además, ha sacado tiempo para hacer 1 hora diaria de ejercicio. ¡Sigue asi!"