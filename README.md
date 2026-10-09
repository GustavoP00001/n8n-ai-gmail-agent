#  Agente Autónomo de Email con n8n y OpenAI

Solución de automatización de extremo a extremo diseñada para la gestión inteligente de consultas por correo electrónico en tiempo real. 

El sistema intercepta mensajes vía Gmail API, analiza la intención de la consulta utilizando **GPT-4o-mini**, mantiene contexto conversacional y responde de forma autónoma con información personalizada.

---

## Herramientas

n8n · Gmail (OAuth2) · OpenAI API (`gpt-4o-mini`) · AI Agent de n8n (LangChain)

## Requisitos previos

- Una instancia de **n8n** (n8n Cloud o instalación propia).
- Una cuenta de **Gmail de prueba**. Recomendado: no uses tu casilla principal.
- Una **API key de OpenAI**. La API se paga por uso.

## Cómo importar y reproducir este proyecto

1. **Descargá el archivo** `n8n-ai-gmail-agent.json` de este repositorio.
2. **Importalo en n8n:** creá un workflow nuevo, abrí el menú de los tres puntos y elegí **Import from file**.
3. **Conectá tus credenciales:**
   - En los nodos **Gmail Trigger** y **Send a message**, creá o elegí tu credencial de Gmail (OAuth2).
   - En el nodo **OpenAI Chat Model**, creá o elegí tu credencial de OpenAI con tu API key.
4. **Configurá el nodo de envío** (ver la sección siguiente).
5. **Probá el workflow** con el workflow inactivo: ejecutalo manualmente y mandá un mail de prueba a tu casilla desde otra cuenta.
6. Cuando todo funcione, **activá el workflow**.

## Configurar el nodo de envío

El nodo **Send a message** viene con datos de ejemplo:

- **To:** `YOUR_EMAIL@example.com`
- **Subject:** `Test subject`
- **Message:** `Example message. Replace this text with the AI Agent output.`

Para usarlo de verdad, cambiá esos campos:

- **To:** poné tu mail o, para responderle a quien escribió, mapealo al remitente del nodo *Gmail Trigger*.
- **Subject:** por ejemplo, `Re:` seguido del asunto original.
- **Message:** mapealo a la salida del nodo **AI Agent** para enviar la respuesta que genera la IA.

Probá cada cambio con un mail de prueba antes de activar el workflow.

## Recomendaciones importantes

- **Filtrá el trigger.** Por defecto no tiene filtros: responde a todos los correos que lleguen. Antes de activarlo, agregá un filtro en el nodo **Gmail Trigger** (por ejemplo, una etiqueta o un remitente específico).
- **Usá una cuenta de prueba** para evitar enviar respuestas automáticas por error.
- **Controlá el costo.** Cada correo procesado hace una llamada a la API de OpenAI.
- **No subas credenciales.** Este repositorio usa placeholders (`YOUR_CREDENTIAL_ID`, `YOUR_EMAIL@example.com`). Si exportás tu propio workflow, revisá que no incluya datos personales antes de publicarlo.

## Personalización

- Cambiá el mensaje del sistema del **AI Agent** para ajustar el tono o el rol (por ejemplo, soporte al cliente o ventas).
- Cambiá el modelo en el nodo **OpenAI Chat Model** según tu presupuesto.
- Agregá nodos para guardar los correos en una planilla o base de datos, o para pedir aprobación antes de enviar.

## Si algo no funciona

- **No se dispara el trigger:** verificá que la credencial de Gmail esté conectada y que haya correos nuevos que cumplan el filtro.
- **Error de OpenAI:** revisá que la API key sea válida y que tu cuenta tenga saldo.
- **No llega la respuesta:** confirmá que el nodo **Send a message** tenga un destinatario real y que el campo **Message** esté mapeado a la salida del agente.
