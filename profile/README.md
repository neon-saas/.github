# Neon

**Catálogo y ventas por WhatsApp con IA para micro y pequeños negocios del Perú.**

Las MIPE peruanas venden por WhatsApp, pero su catálogo no está en ningún sistema: los precios
y el stock viven en la cabeza del dueño, en fotos sueltas de la galería y en un cuaderno. Las
consecuencias son concretas — se responde tarde y se pierde la venta, se vende lo que ya no
hay, y al final del día no se sabe con certeza qué se cobró.

Neon les da un panel donde registran sus productos con precio, stock, descripción e imágenes;
sobre ese catálogo, un agente de IA que atiende por WhatsApp; y a futuro, la consolidación de
los cobros Yape/Plin en un solo lugar.

## Estado

**En construcción — etapa 1.** El plan está cerrado y el código empieza ahora. Lo que sigue
describe el producto completo, con la etapa de cada parte marcada.

## Las tres etapas

Sin catálogo confiable el agente de WhatsApp no tiene nada que responder. Por eso el orden no
es negociable: primero el catálogo, después la conversación, al final el dinero.

| Etapa | Qué entrega |
|---|---|
| **1 · MVP** | Registro del negocio y gestión del catálogo: productos con precio, stock, descripción e imágenes, categorías, búsqueda y ajuste manual de stock con historial de movimientos. |
| **2** | Agente de IA sobre WhatsApp: conexión del número, respuesta a consultas de catálogo, precio y disponibilidad, toma de pedidos y escalamiento a una persona cuando hace falta. |
| **3** | Consolidador de cobros Yape/Plin: registro y conciliación por negocio. |

## Cómo está pensado

- **Mobile-first desde 360 px.** El dueño de una bodega administra su catálogo desde el
  celular, con datos móviles y un teléfono de gama baja. La red inestable es el escenario
  normal, no el raro. No hay app nativa: el panel es web.
- **Aislamiento entre negocios desde el día uno.** Multi-tenant con el identificador del
  negocio saliendo siempre del token, Row Level Security en la base de datos, y un test de
  aislamiento endpoint por endpoint en CI. Tres barreras independientes, porque una sola
  consulta mal filtrada sería el peor incidente posible.
- **Canal oficial de Meta.** WhatsApp Business Cloud API, no librerías no oficiales: son más
  baratas, pero pueden hacer que Meta bloquee el número del cliente — y ese número *es* el
  negocio.
- **Monolito modular, no microservicios.** Lo dicta el equipo, que es de una persona. Lo que
  sí se toma prestado son las fronteras: cada módulo tiene su interfaz pública y ninguno toca
  las tablas de otro.
- **Perú.** PEN, español (`es-PE`), `America/Lima`, y datos personales bajo la Ley N° 29733.

Neon no es un e-commerce: no hay tienda pública ni checkout online. La venta ocurre en
WhatsApp, que es donde ya está el cliente.

## Repositorios

| Repositorio | Descripción | Stack |
|---|---|---|
| [`docs`](https://github.com/neon-saas/docs) | Fuente de verdad del alcance: features, requerimientos, estimaciones, diseño de API y decisiones de arquitectura | — |
| [`neon-api`](https://github.com/neon-saas/neon-api) | API y workers: reglas de negocio, procesado de imágenes, agente y canal de WhatsApp | Kotlin · Ktor · PostgreSQL 17 |
| [`neon-web`](https://github.com/neon-saas/neon-web) | Panel del negocio: catálogo, stock y, en la etapa 2, conversaciones y pedidos | React · TypeScript · Vite |

Dos lenguajes, y es una decisión: el back en Kotlin, el panel en TypeScript porque el
presupuesto de carga en un móvil de gama baja no admite otra cosa. El contrato entre ambos es un
OpenAPI versionado, del que se genera el cliente del panel en CI.

El alcance es igual de explícito: el MVP es exactamente el conjunto de requerimientos `Must`
de `PROYECTO.md`, y nada más.
