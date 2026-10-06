# ⚙️ Proyecto: Automatizaciones con n8n

![Banner Proyectos](https://github.com/user-attachments/assets/94ecebe4-ceba-47ae-8f3c-af14bdfe8606)

## 📋 Planteamiento

Formas parte de un equipo de una consultora tecnológica especializada en automatización de procesos para pequeñas y medianas empresas. Un cliente (una academia, una tienda online, una clínica, una agencia…) pierde cada semana muchas horas en tareas manuales y repetitivas: copiar datos de formularios a hojas de cálculo, responder correos parecidos, enviar recordatorios, generar informes o avisar al equipo cuando pasa algo importante.

Tu equipo debe analizar los procesos del negocio elegido, detectar qué se puede automatizar y diseñar e implementar flujos con **n8n** que conecten las herramientas que el cliente ya usa, reduciendo errores y liberando tiempo para tareas de más valor.

Como en la mayoría de equipos actuales, **el trabajo se hará con agentes de IA**: un agente (como [OpenCode](https://opencode.ai)) con modelos gratuitos ayuda a diseñar, generar y depurar los flujos, y tu equipo hace de *tech lead*: define qué automatizar, da contexto al agente, revisa lo que genera y decide qué se pone en producción. El agente propone, pero la responsabilidad de los flujos es vuestra.

## 🎯 Objetivo

Diseñar e implementar un conjunto de **flujos de automatización con n8n** que resuelvan problemas reales del negocio elegido, integrando varios servicios externos, incorporando **IA** donde aporte valor y quedando documentados y versionados para que el cliente pueda mantenerlos.

## 🛠️ Requisitos Técnicos

1. **n8n** autoalojado (Docker) o n8n Cloud
2. Al menos un disparador por evento (**Webhook**, formulario, correo…) y uno programado (**Schedule Trigger**)
3. Integración con servicios externos (Google Sheets, Gmail, Slack, Telegram, Notion, Airtable, etc.)
4. Gestión segura de **credenciales** en n8n, **nunca escritas en los nodos ni subidas al repositorio**
5. Transformación de datos con nodos nativos (Set/Edit Fields, IF, Switch, Merge…) y nodo **Code** cuando sea necesario
6. Manejo de errores (reintentos, ramas de error y un **Error Workflow**)
7. Flujos exportados en **JSON** y versionados en Git y GitHub
8. Gestión del proyecto con metodologías ágiles (SCRUM)
9. Desarrollo asistido por **agentes de IA** con modelos gratuitos (ver sección siguiente)

## 🤖 Desarrollo Agéntico con IA

El proyecto debe desarrollarse con un agente de IA en la terminal, trabajando como se hace hoy en la industria.

**Herramientas**

- Agente: **[OpenCode](https://opencode.ai)** (recomendado). Se pueden usar alternativas abiertas o gratuitas (Aider, Cline, Kilo Code…), pero hay que justificar la elección.
- Modelos **gratuitos**, por ejemplo: los modelos gratuitos de OpenCode Zen, modelos `:free` de OpenRouter, la capa gratuita de Groq o Gemini, o modelos locales con **Ollama**. Los mismos modelos se pueden usar dentro de n8n en los nodos de IA.
- Si tienen IAs de pago pueden utilizarlas, solo que tenerlo en cuenta para no pisar el trabajo del equipo, delimitar muy bien el alcance que tendrán.

**Forma de trabajo**

1. **Contexto antes que flujos:** crear un `AGENTS.md` en la raíz con el negocio, los servicios integrados, las convenciones de nombres de flujos y nodos, cómo importar y exportar flujos y lo que el agente **no** debe hacer (por ejemplo: no escribir credenciales en el JSON, no activar flujos en producción).
2. **SDD & Ontologías:** antes de pedirle nada al agente, cada automatización se define con *Spec-Driven Development* en una spec (`specs/`) con el disparador, las entradas, las salidas, los casos de error y los criterios de aceptación, apoyada en una ontología del dominio: entidades del negocio (`Cliente`, `Pedido`, `Reserva`…), sus atributos, relaciones y reglas. Así el agente y el equipo comparten el mismo vocabulario y no inventan conceptos.
3. **Tareas pequeñas:** una tarea del Kanban equivale a un flujo (o parte de uno), una rama y una Pull Request con el JSON exportado.
4. **Revisión humana obligatoria:** todo flujo generado se importa, se prueba con datos de ejemplo y se revisa en la PR antes de mergear. Hay que prestar especial atención a la seguridad: credenciales, datos personales y webhooks expuestos.
5. **Pruebas como contrato:** cada flujo tiene datos de prueba (pinned data o payloads de ejemplo) y un resultado esperado. Si una prueba falla, se arregla el flujo, no se cambia la prueba.
6. **Trazabilidad:** registrar los prompts más relevantes y las decisiones que se tomaron (qué se aceptó, qué se rechazó y por qué).

## 📦 Entregables

1. Mapa de procesos del cliente: situación actual y procesos automatizados (diagrama BPMN, Miro, Excalidraw o similar)
2. Repositorio en GitHub con los flujos exportados en JSON y README con instrucciones para importarlos y configurarlos
3. Documentación de cada flujo: objetivo, disparador, servicios que usa, credenciales necesarias y capturas
4. `.env.example` y, si es autoalojado, `docker-compose.yml` para levantar n8n
5. Datos de prueba y evidencias de ejecución (capturas o vídeo de las ejecuciones)
6. Documento de retrospectiva del proyecto
7. Tablero Kanban (Trello, Jira, GitHub Projects, etc.) con historias de usuario
8. `AGENTS.md` y carpeta `specs/` con las especificaciones de cada automatización
9. **Bitácora de IA** (`docs/ai-log.md`): herramienta y modelos usados, prompts clave, errores o alucinaciones del agente y cómo se corrigieron
10. Historial de PRs con revisiones visibles de los flujos generados

## 🏆 Niveles de Entrega

### 🟢 Nivel Esencial

- Mínimo 3 flujos funcionales que resuelvan procesos reales del negocio
- Al menos un flujo con disparador por evento (Webhook o formulario) y otro programado
- Integración con al menos 2 servicios externos (por ejemplo: formulario → Google Sheets → notificación por Gmail o Slack)
- Uso de lógica condicional (IF / Switch) y transformación de datos
- Credenciales gestionadas en n8n y variables de entorno para datos sensibles
- Manejo de errores básico con un Error Workflow que avise al equipo
- Flujos exportados en JSON y versionados en GitHub
- Gestión de proyecto con Kanban
- `AGENTS.md` funcional y bitácora de IA con al menos los prompts de cada flujo principal

### 🟡 Nivel Medio

- 5 o más flujos, incluyendo sub-workflows reutilizables (**Execute Workflow**)
- Consumo de una API REST externa con el nodo **HTTP Request** (autenticación, paginación…)
- Nodos de **IA** (AI Agent, Basic LLM Chain…) con un modelo gratuito para clasificar, resumir o generar respuestas
- Reintentos configurados y control de errores por nodo
- Generación de informes periódicos (CSV, PDF o correo resumen)
- Flujo spec → agente → PR → revisión aplicado a todas las automatizaciones
- Comparativa de al menos 2 modelos gratuitos en una misma tarea (calidad, velocidad, errores)

### 🟠 Nivel Avanzado

- **Agente de IA** en n8n con memoria y herramientas (consultar una hoja, una base de datos o una API) conectado a un canal (Telegram, Slack, chat web…)
- **RAG** sencillo con una base vectorial (Supabase, Qdrant, Pinecone…) sobre documentación del negocio
- Persistencia en base de datos (PostgreSQL, Supabase…) en lugar de solo hojas de cálculo
- Webhooks protegidos (autenticación por cabecera o token) y validación de los datos de entrada
- Gestión de datos personales conforme al RGPD (minimización, borrado, no enviar datos sensibles a modelos externos)
- Uso de **MCP** para que el agente (OpenCode) consulte o cree flujos en n8n
- Comandos, skills o subagentes personalizados en OpenCode para tareas repetitivas (generar specs, revisar flujos…)

### 🔴 Nivel Experto

- n8n autoalojado con **Docker** y `docker-compose` (n8n + PostgreSQL), con volúmenes y copias de seguridad
- Despliegue en la nube (Render, Railway, un VPS, Google Cloud, etc.) con HTTPS
- Modo cola (**queue mode** con Redis y workers) para flujos con mucha carga
- Pipeline de CI con GitHub Actions que valide los JSON de los flujos en cada PR
- Despliegue de flujos entre entornos (desarrollo → producción) mediante la API de n8n
- Exponer un flujo como servidor MCP (**MCP Server Trigger**) para que otros agentes lo usen como herramienta
- Panel o interfaz básica para que el cliente vea el estado y los resultados de las automatizaciones
