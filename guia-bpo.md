# Guia Claude para BPO / Cowork — negocio / no tecnico

> **Track secundario** de este kit. Para Legal, RRHH, operaciones, back office,
> finanzas operativas y managers. Superficie principal: **Claude Cowork** + Chat +
> skills/plugins/conectores. Sin terminal, sin codigo.
>
> Esta guia es autocontenida: si solo te interesa la parte de negocio, lees esto y
> no necesitas el track tecnico. Para el resumen/indice y el track Code, ver
> [`claude-guide.md`](claude-guide.md) (central) y [`guia-code.md`](guia-code.md).

## Lectura minima (si solo hay tiempo para 4 piezas)

| Prioridad | Fuente | Por que importa |
|---|---|---|
| 1 | [Get started with Claude Cowork](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork) | Manual oficial: como empezar, permisos, proyectos y modos de operacion. |
| 2 | [Use Claude Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely) | Base para guardrails: file access, scope creep, scheduled tasks, datos sensibles. |
| 3 | [Set up Claude Cowork to work the way you do](https://claude.com/resources/tutorials/cowork-onboarding-guide) | Explica Cowork Project, folder, tools, browser, instrucciones y plugins. |
| 4 | [Claude for Human Resources](https://claude.com/resources/tutorials/claude-for-human-resources) | Ejemplos oficiales por funcion (RRHH); modelo replicable para otras areas. |

## Guia oficial principal

| Fuente | Resumen util para capacitacion |
|---|---|
| [Get started with Claude Cowork](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork) | Punto de partida para usuarios: Cowork corre desde Claude Desktop, trabaja con archivos y proyectos, y requiere configurar acceso. |
| [Delegating your first task in Claude Cowork](https://claude.com/resources/tutorials/delegating-your-first-task-in-claude-cowork) | Sirve como demo inicial: dar acceso a carpeta/conectores, delegar una tarea completa y revisar el plan antes de cambios. |
| [Set up Claude Cowork to work the way you do](https://claude.com/resources/tutorials/cowork-onboarding-guide) | Muy buena para explicar proyectos, contexto, instrucciones, conectores, plugins y scheduled tasks. |
| [Choosing between Claude Cowork or Chat](https://claude.com/resources/tutorials/choosing-between-claude-cowork-or-chat) | Ayuda a evitar confusion: Chat para conversaciones; Cowork para trabajo con archivos, herramientas y tareas. |
| [Use Claude Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely) | Debe estar en todo training corporativo: acceso selectivo a archivos, monitoreo de tareas, cuidado con scheduled tasks. |
| [Organize your tasks with projects in Claude Cowork](https://support.claude.com/en/articles/14116274-organize-your-tasks-with-projects-in-claude-cowork) | Para ensenar que cada equipo debe tener un workspace ordenado, no tareas sueltas. |
| [Use Claude Cowork on Team and Enterprise plans](https://support.claude.com/en/articles/13455879-use-claude-cowork-on-team-and-enterprise-plans) | Para administradores y champions: condiciones de despliegue en Team/Enterprise. |
| [Claude Cowork desktop architecture overview](https://support.claude.com/en/articles/14479288-claude-cowork-desktop-architecture-overview) | Importante para seguridad: la arquitectura y la visibilidad de endpoint/security tooling deben entenderse antes del rollout. |

## Guias oficiales por funcion

| Funcion | Fuente | Que sacar para la capacitacion |
|---|---|---|
| RRHH | [Claude for Human Resources](https://claude.com/resources/tutorials/claude-for-human-resources) | Politicas, comunicaciones, interview prep, employee communications. Usar como base para RRHH/BPO People. |
| RRHH/Excel | [How to use Claude in Excel for HR: Headcount planning](https://claude.com/resources/tutorials/how-to-use-claude-in-excel-for-hr-headcount-planning) | Buen puente para usuarios de Excel: planeamiento, tablas, escenarios y resumen. |
| Legal | [Using Claude Cowork for legal: answer fast questions on past decisions](https://claude.com/resources/tutorials/using-claude-cowork-for-legal-question-briefing) | Caso canonico de Legal: responder preguntas sobre decisiones previas usando documentos y contexto. |
| Legal/plugins | [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) | Suite oficial de plugins/skills legales: commercial legal, employment legal, privacy/compliance, litigation support. |
| Knowledge work | [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) | Repositorio oficial de plugins para trabajadores de conocimiento; built for Cowork y compatible con Code. |
| **Small business** ★ | [Claude for Small Business (anuncio)](https://www.anthropic.com/news/claude-for-small-business) · [solutions page](https://claude.com/solutions/small-business) | **Paquete oficial Anthropic para back-office no tecnico** (13-may-2026): 15 workflows agenticos + 15 skills listos por funcion (payroll/cierre mensual/forecast, lead triage, dashboards). Conectores QuickBooks, PayPal, HubSpot, Canva, DocuSign, Google Workspace, M365. **El mejor ejemplo "listo para usar" para BPO.** |
| **Founder / startup** ★ | [The Founder's Playbook](https://claude.com/blog/the-founders-playbook) | **Guia oficial Anthropic para founders** (14-may-2026): mapea el uso de Claude por etapa de startup — Idea, MVP, Launch, Scale — con frameworks, ejercicios y prompts. Tesis: el founder pasa de "individual contributor" a "orchestrator" (Claude hace dev inicial, automatizacion de workflows y operaciones; el humano se queda con lo estrategico). Casos: Ambral, Carta Healthcare, HumanLayer. **Base para recomendar a un founder solo sin equipo.** |
| Administradores | [Claude Enterprise Administrator Guide](https://claude.com/resources/tutorials/claude-enterprise-administrator-guide) | Para owners/admins: adopcion, politicas, rollout, ejemplos por funcion. |

## Buenas practicas BPO / Cowork

Estas buenas practicas salen de las guias oficiales anteriores, no de inventar un
framework nuevo:

1. **Empezar con una carpeta dedicada**: no dar acceso amplio al disco. Cowork es
   mas facil de supervisar cuando trabaja en un folder de tarea/proyecto.
2. **Configurar Project instructions**: rol, formato esperado, tono, restricciones,
   fuentes permitidas y que debe preguntar antes de acciones sensibles.
3. **Usar plugins/skills antes de prompts sueltos**: Legal/RRHH/ops funcionan
   mejor con playbooks que con instrucciones improvisadas.
4. **Revisar el plan antes de ejecutar**: Cowork puede hacer cambios; el usuario
   debe mirar si la tarea se esta expandiendo fuera del alcance.
5. **Pedir evidencias/citas**: archivo, seccion, fila, fecha o fuente. Sin cita,
   el output es borrador, no respuesta final.
6. **No usarlo para decisiones finales**: contratacion, despido, sancion, pago,
   aprobacion legal, cambios regulatorios o comunicaciones sensibles requieren
   responsable humano.
7. **Scheduled tasks solo para procesos claros**: resumen semanal, monitoreo de
   carpeta, briefing; no para acciones irreversibles.

## Seguridad — el riesgo es **acceso y acciones**, no codigo

> Fuente oficial: [Use Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely).

A esta audiencia no le hables de `.env` ni de permisos en JSON. Su modelo mental
es "un asistente con acceso a mis archivos y herramientas". Las preguntas reales:

1. **"¿Puede ver TODO mi ordenador?"** → No si lo configuras bien. Regla #1
   (oficial): **carpeta dedicada**, no acceso amplio. Lo que no esta en la carpeta,
   no lo ve. Mantener backups de lo importante.
2. **"¿Y si borra o manda algo por error?"** → Cowork **pide permiso explicito**
   antes de borrar definitivamente (prompt "Allow"). Regla: revisar el **plan
   antes** de ejecutar, y vigilar **scope creep** (¿accede a archivos/webs que no
   mencionaste? -> parar). El modo "Act without asking" **sube mucho** el riesgo
   de prompt injection: solo bajo supervision activa.
3. **"¿Manda emails / hace compras solo?"** → No debe. Configurar **preparar
   borrador, nunca enviar/comprar/publicar** sin confirmacion. Esto se fija en las
   instrucciones base (manual del asistente).
4. **"¿Y los datos sensibles de la empresa?"** → No darle acceso a documentos con
   credenciales, datos financieros o PII salvo necesidad clara y anonimizada.
   Evitar Claude-en-Chrome para informacion sensible. Respetar las politicas de la
   empresa (si no se permite, esa es otra conversacion con IT/seguridad).
5. **"¿Las tareas programadas no se descontrolan?"** → Empezar simple (resumenes,
   recopilar info), nunca acciones dificiles de deshacer en automatico. Revisar
   outputs y pausar las que no se usan.
6. **Conectores/plugins**: solo los del directorio verificado de Claude; evaluar
   los permisos que pide cada extension antes de instalar.

**Mensaje de una linea para BPO:** *"Cowork mira, resume y prepara; tu decides y
confirmas. Carpeta acotada + revisar el plan + nada irreversible en automatico."*

> **Principio comun con Code:** minimo privilegio + humano en las decisiones
> irreversibles. En BPO se expresa como carpeta acotada y confirmacion; en Code
> como permisos, `deny` y hooks. Mismo concepto, distinto vocabulario.

## Videos YouTube recomendados para BPO/Cowork

Datos consultados con YouTube Data API el 2026-06-19. Los conteos cambian.
Ordenado por relevancia para usuarios no tecnicos, no solo por vistas.

| Prioridad | Video | Canal | Duracion | Views | Likes | Uso recomendado |
|---|---|---:|---:|---:|---:|---|
| 1 | [Introducing Cowork: Claude Code for the rest of your work](https://www.youtube.com/watch?v=UAmKyyZ-b9E) | Anthropic | 1:09 | 753K | 6.8K | Intro oficial para abrir la capacitacion. |
| ★ ES | [Tutorial completo de Claude Co-work: de cero a avanzado](https://www.youtube.com/watch?v=exZfoIxHKEQ) | Migue Baena IA | 32:50 | 24.8K | 909 | **Pieza base BPO en espanol.** Zero-to-advanced con seguridad primero: carpeta dedicada, instrucciones base, `mi-contexto/` (perfil/escritura/memoria), conectores, skills vs plugins vs tareas programadas. Replicar su escalera. |
| 2 | [Learn 80% of Claude Cowork in Under 20 Minutes](https://www.youtube.com/watch?v=z9rdrNrkvDY) | Jeff Su | 18:55 | 1.04M | 20.3K | Mejor prework general para usuarios de negocio. |
| 3 | [Claude COWORK Clearly Explained](https://www.youtube.com/watch?v=ZeWfksNXlbU) | Eliot Prince | 18:29 | 967K | 12.6K | Explicacion clara para principiantes; buen puente Chat vs Cowork. |
| 4 | [Set Up Claude Cowork better than 99% of people](https://www.youtube.com/watch?v=pl90LATQlHI) | Systems Made Better | 47:53 | 503K | 10.4K | Bueno para champions/power users, no para todos. |
| 5 | [Claude Cowork Full Tutorial](https://www.youtube.com/watch?v=vMo-yRCN3QM) | Bart Slodyczka | 14:23 | 312K | 4.8K | Resumen de workflow, plugins y tareas. |
| 6 | [How to Use Claude Cowork Better Than 99% of People](https://www.youtube.com/watch?v=f95-O8C88uw) | AI for Non Techies | 20:43 | 206K | 4.8K | Muy alineado con audiencia no tecnica; lenguaje accesible. |
| 7 | [Claude Cowork - Full Course for Beginners](https://www.youtube.com/watch?v=tf_KmDNZXzI) | Tech With Tim | 24:16 | 164K | 2.7K | Buen video si alguien quiere entender diferencias con Claude Code. |

## Posts X/LinkedIn utiles para BPO

Notas:

- X/LinkedIn cambian metricas y pueden ocultar contenido segun login.
- Estos links son ejemplos para inspirar slides o casos; no son fuente normativa.

| Fuente | Tema | Por que sirve |
|---|---|---|
| [@alliekmiller - Legal plugin / `/legal:triage-nda`](https://x.com/alliekmiller/status/2021586268573024337) | Legal plugin aplicado a NDA triage. | Ejemplo visual de un skill real de Legal. |
| [@law_ninja - lawyers should use Claude Cowork smartly](https://x.com/law_ninja/status/2026263310661021773) | Legal, contract review, compliance workflows. | Buen framing para Legal: acelerar revision, no reemplazar criterio. |
| [HelloParalegal - What Claude Cowork Actually Is](https://x.com/helloparalegal/article/2028449520498164172) | Legal operations y paralegal work. | Caso BPO/legal: reducir primera revision y dejar humana la decision. |
| [@coreyganim - 21 Claude Cowork plugins](https://x.com/coreyganim/status/2027481262668054788) | Plugins de Cowork por funcion. | Sirve para mostrar amplitud: legal, finance, ops, etc. |
| [@RyanJAyala - Cowork for non-technical people](https://x.com/RyanJAyala/status/2029942669527470087) | Cowork como "Claude Code sin terminal". | Mensaje simple para adopcion. |
| [Hannah Stulberg - CLAUDE.md files](https://www.linkedin.com/posts/hannah-stulberg_claudemd-files-are-the-most-underused-feature-activity-7426982758331199488-UZzF) | Instrucciones persistentes para Claude. | Llevar a BPO como "instrucciones del area / playbook". |

## Skills/plugins que conviene mostrar (BPO / Cowork)

| Recurso | Fuente | Para quien | Que mostrar |
|---|---|---|---|
| **Claude for Small Business** ★ | [anuncio](https://www.anthropic.com/news/claude-for-small-business) · [solutions](https://claude.com/solutions/small-business) | Duenos/equipos de back-office | 15 workflows + 15 skills listos (payroll, cierre mensual, forecast, lead triage, dashboards). Demo "listo para usar" mas convincente para BPO no tecnico. Aprobacion del usuario antes de actuar; respeta permisos existentes. |
| Knowledge Work Plugins | [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) | Legal, finance, ops, marketing, sales | Plugins por rol: no empezar desde prompt vacio. |
| Claude for Legal | [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) | Legal/compliance | Commercial legal, employment legal, privacy/compliance, litigation support. |
| Legal vendor agreement review | [vendor-agreement-review skill](https://github.com/anthropics/claude-for-legal/blob/main/commercial-legal/skills/vendor-agreement-review/SKILL.md) | Procurement/legal | Severidad contra playbook: Critical/High/Medium, no opinion suelta. |
| Employment hiring review | [hiring-review skill](https://github.com/anthropics/claude-for-legal/blob/main/employment-legal/skills/hiring-review/SKILL.md) | HR/legal | Offer letters, jurisdiction checks, restrictive covenants, citas y contexto. |
| Skills directory | [Browse skills, connectors, and plugins](https://support.claude.com/en/articles/14328846-browse-skills-connectors-and-plugins-in-one-directory) | Admins/champions | Como descubrir y provisionar recursos. |
| Organization skills management | [Provision and manage skills](https://support.claude.com/en/articles/13119606-provision-and-manage-skills-for-your-organization) | Owners/admins | Compartir skills deliberadamente; revisar antes de org-wide sharing. |

## Sesiones de capacitacion — BPO/Cowork

### Sesion 1 — "No es chat, es delegacion supervisada"

Prework:

- Video oficial: [Introducing Cowork](https://www.youtube.com/watch?v=UAmKyyZ-b9E)
- Guia oficial: [Delegating your first task](https://claude.com/resources/tutorials/delegating-your-first-task-in-claude-cowork)
- Seguridad: [Use Claude Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely)

Demo:

- Crear proyecto con carpeta dedicada.
- Conectar una fuente controlada.
- Delegar una tarea con output verificable.
- Revisar plan y resultado.

### Sesion 2 — BPO por funcion: Legal/RRHH/Ops

Prework:

- [Claude for Human Resources](https://claude.com/resources/tutorials/claude-for-human-resources)
- [Using Claude Cowork for legal](https://claude.com/resources/tutorials/using-claude-cowork-for-legal-question-briefing)
- [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal)

Demo:

- Legal: NDA triage o vendor agreement review.
- RRHH: politica interna con citas o headcount planning en Excel.
- Ops: QA de casos contra checklist.
