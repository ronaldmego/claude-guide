# Guía Claude sin código (Cowork / Chat) — para tu trabajo diario

> Si no escribes código, igual puedes delegar trabajo real a Claude vía **Claude
> Cowork** y **Chat**: sin terminal, sin programar. Esta guía es autocontenida.
>
> Su superficie principal es **Cowork** (Claude trabajando con tus archivos y
> herramientas) más **Chat** (conversación). Para el índice general y el otro
> track —**si programas** (Claude Code)— ver
> [`claude-kit.md`](../claude-kit.md) (central) y
> [`guia-code.md`](../code-data/guia-code.md).

## Lectura mínima (si solo hay tiempo para 4 piezas)

| Prioridad | Fuente | Por qué importa |
|---|---|---|
| 1 | [Get started with Claude Cowork](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork) | Manual oficial: cómo empezar, permisos, proyectos y modos de operación. |
| 2 | [Use Claude Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely) | Base de seguridad: acceso a archivos, scope creep, tareas programadas, datos delicados. |
| 3 | [Set up Claude Cowork to work the way you do](https://claude.com/resources/tutorials/cowork-onboarding-guide) | Explica el Cowork Project: carpeta, herramientas, navegador, instrucciones y plugins. |
| 4 | [Choosing between Claude Cowork or Chat](https://claude.com/resources/tutorials/choosing-between-claude-cowork-or-chat) | Te ayuda a elegir la herramienta correcta: Chat para conversar, Cowork para trabajar con archivos. |

## Guía oficial principal

| Fuente | Para qué te sirve |
|---|---|
| [Get started with Claude Cowork](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork) | Punto de partida: Cowork corre desde Claude Desktop, trabaja con tus archivos y proyectos, y requiere que configures su acceso. |
| [Delegating your first task in Claude Cowork](https://claude.com/resources/tutorials/delegating-your-first-task-in-claude-cowork) | Tu primera prueba: darle acceso a una carpeta/conector, delegar una tarea completa y revisar el plan antes de que cambie nada. |
| [Set up Claude Cowork to work the way you do](https://claude.com/resources/tutorials/cowork-onboarding-guide) | Cómo dejar Cowork a tu medida: proyectos, contexto, instrucciones, conectores, plugins y tareas programadas. |
| [Choosing between Claude Cowork or Chat](https://claude.com/resources/tutorials/choosing-between-claude-cowork-or-chat) | Evita la confusión: Chat para conversaciones; Cowork para trabajo con archivos, herramientas y tareas. |
| [Use Claude Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely) | Léela sí o sí: acceso selectivo a archivos, revisar lo que hace, cuidado con las tareas programadas. |
| [Organize your tasks with projects in Claude Cowork](https://support.claude.com/en/articles/14116274-organize-your-tasks-with-projects-in-claude-cowork) | Cómo tener un espacio ordenado por proyecto en vez de tareas sueltas y perdidas. |
| [Claude Cowork desktop architecture overview](https://support.claude.com/en/articles/14479288-claude-cowork-desktop-architecture-overview) | Si te interesa la parte de seguridad: cómo funciona Cowork por dentro y qué ve en tu equipo. |

## Ejemplos de tareas reales (no técnicas)

No necesitas ser de ninguna "área": son tareas cotidianas que Cowork puede hacer
por ti. Estas fuentes oficiales sirven como modelo replicable para lo que tú
necesites.

| Tarea | Fuente | Qué aprender de ahí |
|---|---|---|
| Planear en Excel (escenarios, tablas) | [How to use Claude in Excel: Headcount planning](https://claude.com/resources/tutorials/how-to-use-claude-in-excel-for-hr-headcount-planning) | Buen puente si vives en Excel: planeamiento, tablas, escenarios y resúmenes. Replica el método para tu presupuesto, proyecto o cálculo personal. |
| Responder preguntas sobre tus propios documentos | [Using Claude Cowork to answer fast questions on past decisions](https://claude.com/resources/tutorials/using-claude-cowork-for-legal-question-briefing) | Caso canónico: hacerle preguntas a tus documentos y notas para recuperar rápido algo que ya decidiste o guardaste. |
| Arrancar con playbooks en vez de prompts en blanco | [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) | Repositorio oficial de plugins para trabajo de conocimiento; hecho para Cowork y compatible con Code. Toma prestado el que te sirva. |
| **Si trabajas por tu cuenta / tienes tu emprendimiento** ★ | [Claude for Small Business (anuncio)](https://www.anthropic.com/news/claude-for-small-business) · [solutions](https://claude.com/solutions/small-business) | Paquete oficial de Anthropic (13-may-2026): 15 workflows y 15 skills listos (facturación, cierre de mes, forecast, seguimiento de clientes, dashboards). Conectores QuickBooks, PayPal, HubSpot, Canva, DocuSign, Google Workspace, M365. **El mejor punto de partida "listo para usar" si llevas tú solo la parte administrativa.** |
| **Si estás montando algo desde cero (founder solo)** ★ | [The Founder's Playbook](https://claude.com/blog/the-founders-playbook) | Guía oficial (14-may-2026): usa Claude por etapa —Idea, MVP, Launch, Scale— con frameworks, ejercicios y prompts. Tesis: pasas de hacer todo tú a *orquestar* (Claude toma la parte repetitiva y operativa; tú te quedas con lo estratégico). Casos: Ambral, Carta Healthcare, HumanLayer. |

## Buenas prácticas (Cowork / Chat)

Estas salen de las guías oficiales anteriores, no de inventar un framework nuevo:

1. **Empieza con una carpeta dedicada**: no le des acceso amplio a todo el disco.
   Cowork es más fácil de supervisar cuando trabaja en la carpeta de una tarea o
   proyecto concreto.
2. **Configura las instrucciones del proyecto**: qué esperas, formato, tono,
   restricciones, qué fuentes puede usar y qué debe preguntarte antes de hacer
   algo delicado.
3. **Usa plugins/skills antes que prompts sueltos**: muchas tareas salen mejor con
   un playbook listo que con instrucciones improvisadas.
4. **Revisa el plan antes de ejecutar**: Cowork puede hacer cambios; mira si la
   tarea se está saliendo de lo que pediste.
5. **Pide evidencias/citas**: archivo, sección, fila, fecha o fuente. Sin cita, el
   resultado es un borrador, no una respuesta final.
6. **No lo uses para decisiones finales irreversibles**: firmar algo, pagar,
   publicar, borrar definitivo o mandar un correo importante los decides y
   confirmas tú.
7. **Tareas programadas solo para procesos claros**: un resumen semanal, vigilar
   una carpeta, un briefing; nunca para acciones difíciles de deshacer.

## Seguridad — el riesgo es **acceso y acciones**, no codigo

> Fuente oficial: [Use Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely).

Aquí no hace falta hablar de `.env` ni de permisos en JSON. El modelo mental es
"un asistente con acceso a mis archivos y herramientas". Las preguntas reales:

1. **"¿Puede ver TODO mi ordenador?"** → No si lo configuras bien. Regla #1
   (oficial): **carpeta dedicada**, no acceso amplio. Lo que no está en la carpeta,
   no lo ve. Mantén backups de lo importante.
2. **"¿Y si borra o manda algo por error?"** → Cowork **pide permiso explícito**
   antes de borrar definitivamente (prompt "Allow"). Regla: revisa el **plan
   antes** de ejecutar, y vigila el **scope creep** (¿accede a archivos/webs que no
   mencionaste? → para). El modo "Act without asking" **sube mucho** el riesgo de
   prompt injection: úsalo solo bajo supervisión activa.
3. **"¿Manda emails / hace compras solo?"** → No debe. Configúralo para **preparar
   borradores, nunca enviar/comprar/publicar** sin tu confirmación. Esto se fija en
   las instrucciones base del asistente.
4. **"¿Y mis datos delicados?"** → No le des acceso a documentos con contraseñas,
   datos financieros o información personal salvo necesidad clara. Evita
   Claude-en-Chrome para información sensible.
5. **"¿Las tareas programadas no se descontrolan?"** → Empieza simple (resúmenes,
   recopilar info), nunca acciones difíciles de deshacer en automático. Revisa los
   resultados y pausa las que no uses.
6. **Conectores/plugins**: solo los del directorio verificado de Claude; revisa qué
   permisos pide cada extensión antes de instalar.

**Resumen en una línea:** *"Cowork mira, resume y prepara; tú decides y confirmas.
Carpeta acotada + revisar el plan + nada irreversible en automático."*

> **Principio común con el track de código:** mínimo privilegio + humano en las
> decisiones irreversibles. Sin código se expresa como carpeta acotada y
> confirmación; con Claude Code como permisos, `deny` y hooks. Mismo concepto,
> distinto vocabulario.

## Videos de YouTube recomendados

Datos consultados con la YouTube Data API el 2026-06-19. Los conteos cambian.
Ordenado por utilidad para alguien no técnico, no solo por vistas.

| Prioridad | Video | Canal | Duración | Views | Likes | Para qué |
|---|---|---:|---:|---:|---:|---|
| 1 | [Introducing Cowork: Claude Code for the rest of your work](https://www.youtube.com/watch?v=UAmKyyZ-b9E) | Anthropic | 1:09 | 753K | 6.8K | Intro oficial de 1 minuto para entender la idea. |
| ★ ES | [Tutorial completo de Claude Co-work: de cero a avanzado](https://www.youtube.com/watch?v=exZfoIxHKEQ) | Migue Baena IA | 32:50 | 24.8K | 909 | **Tu mejor punto de partida en español.** De cero a avanzado, seguridad primero: carpeta dedicada, instrucciones base, `mi-contexto/` (perfil/escritura/memoria), conectores, skills vs plugins vs tareas programadas. Replica su escalera. |
| 2 | [Learn 80% of Claude Cowork in Under 20 Minutes](https://www.youtube.com/watch?v=z9rdrNrkvDY) | Jeff Su | 18:55 | 1.04M | 20.3K | El mejor repaso general en poco tiempo. |
| 3 | [Claude COWORK Clearly Explained](https://www.youtube.com/watch?v=ZeWfksNXlbU) | Eliot Prince | 18:29 | 967K | 12.6K | Explicación clara para principiantes; buen puente Chat vs Cowork. |
| 4 | [Set Up Claude Cowork better than 99% of people](https://www.youtube.com/watch?v=pl90LATQlHI) | Systems Made Better | 47:53 | 503K | 10.4K | Para cuando quieras profundizar; largo. |
| 5 | [Claude Cowork Full Tutorial](https://www.youtube.com/watch?v=vMo-yRCN3QM) | Bart Slodyczka | 14:23 | 312K | 4.8K | Resumen de flujo de trabajo, plugins y tareas. |
| 6 | [How to Use Claude Cowork Better Than 99% of People](https://www.youtube.com/watch?v=f95-O8C88uw) | AI for Non Techies | 20:43 | 206K | 4.8K | Muy alineado con audiencia no técnica; lenguaje accesible. |
| 7 | [Claude Cowork - Full Course for Beginners](https://www.youtube.com/watch?v=tf_KmDNZXzI) | Tech With Tim | 24:16 | 164K | 2.7K | Bueno si quieres entender la diferencia con Claude Code. |

## Ruta de aprendizaje sugerida

Un camino simple para arrancar sin abrumarte:

1. **Entiende la idea** (10 min): el video oficial [Introducing Cowork](https://www.youtube.com/watch?v=UAmKyyZ-b9E)
   y [Choosing between Cowork or Chat](https://claude.com/resources/tutorials/choosing-between-claude-cowork-or-chat).
2. **Tu primera tarea** (30 min): sigue [Delegating your first task](https://claude.com/resources/tutorials/delegating-your-first-task-in-claude-cowork)
   — crea un proyecto con **una carpeta dedicada**, delega algo pequeño con un
   resultado que puedas verificar y revisa el plan antes de que cambie nada.
3. **Hazlo tuyo** (1 h): el tutorial en español de [Migue Baena](https://www.youtube.com/watch?v=exZfoIxHKEQ)
   para configurar instrucciones base, contexto y conectores a tu medida.
4. **Refuerza la seguridad**: repasa [Use Claude Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely)
   y aplica la regla de una línea: *mira, resume y prepara; tú decides y confirmas.*
