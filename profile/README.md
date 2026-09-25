# Neon

**Ventas por WhatsApp con IA para pequeños y medianos negocios en Perú.**

Neon es un SaaS multi-tenant que conecta el WhatsApp Business de cada negocio con un asistente de IA que atiende a sus clientes, ofrece su catálogo y cierra ventas, mientras el dueño supervisa todo desde un panel web.

## ¿Qué hace?

- 💬 **Atención por WhatsApp con IA**: responde a los clientes con el contexto y el catálogo actualizado de cada negocio.
- 🛒 **Catálogo en tiempo real**: productos, precios y stock que el asistente ofrece al instante.
- 🙋 **Handoff humano**: cuando la IA lo necesita, el dueño toma la conversación desde el panel.
- 💸 **Pagos con Yape, Plin y transferencia**: registro de comprobantes enviados por WhatsApp para su revisión.

## Componentes

| Repositorio | Descripción | Stack |
|---|---|---|
| `neon-api` | Backend multi-tenant, webhook de WhatsApp Cloud API e integración con el LLM | FastAPI · PostgreSQL · Claude |
| `neon-web` | Panel para los negocios: catálogo, conversaciones y pagos | Astro · TypeScript |
