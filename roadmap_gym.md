# Emma Velázquez - Shopify Development Roadmap 2026

Este documento detalla la planificación estratégica y técnica para el desarrollo y optimización del sitio Shopify de **Emma Velázquez**. El objetivo es escalar el sitio actual hacia una plataforma omnicanal "vitaminada" que soporte nativamente operaciones de **Retail (B2C), Mayoreo (B2B) y Sistema de Rentas**, sin depender de exceso de aplicaciones de terceros que afecten el rendimiento.

---

## 🚀 Plan de Ejecución (Fases Numeradas)

### 1. Fase 1: Arquitectura de Datos y Filtros Nativos (Fundamentos)
Para soportar catálogos tan diferentes (Venta vs. Renta vs. Mayoreo) necesitamos una base de datos impecable usando la tecnología nativa de Shopify 2.0.

*   **1.1. Configuración de Metafields & Metaobjects:** Crear estructuras de datos nativas para:
    *   *Producto:* Momento de Uso, Silueta, Textura, Tipo de Operación (Venta / Renta).
    *   *Cliente:* Tipo de Perfil (B2C, B2B, Novia), Nivel de Descuento.
*   **1.2. Facetas y Filtros Nativos:** Implementar los nuevos Metafields en la aplicación *Shopify Search & Discovery* (Nativa) para eliminar apps de terceros de filtrado. Esto acelerará las páginas de colección (PLP).
*   **1.3. Search Predictivo Visual:** Optimizar la barra de búsqueda del tema Symmetry para que indexe los Metafields técnicos y muestre resultados más precisos de inmediato.

### 2. Fase 2: Arquitectura de Navegación y Segmentación
El usuario debe tener claro desde el segundo uno si está comprando, rentando o en el portal de mayoreo.

*   **2.1. Mega Menú de Intención:** Refactorizar el header (`header.liquid`) para separar los flujos principales. Implementar una jerarquía por "Momento de Uso" (Bodas, Graduaciones) y "Servicio" (Compra vs. Renta).
*   **2.2. Home Page "Bento Grid":** Reconstruir el `index.json` usando una estructura tipo Bento Grid para segmentar audiencias visualmente (un bloque para Renta, otro para Mayoreo, otro para Novedades Retail).

### 3. Fase 3: Ecosistema de Rentas (Desarrollo Nativo)
Crear un sistema de rentas fluido usando Liquid y JS, sin apps de terceros que cobren suscripción mensual por reservaciones.

*   **3.1. Calendario de Reservaciones en PDP:** Integrar un selector de fechas (Datepicker JS) directamente en `main-product.liquid`. Las fechas se guardarán como **Line Item Properties** ocultas (`_Fecha_Inicio`, `_Fecha_Fin`) para viajar al carrito y al pedido.
*   **3.2. Lógica de Depósito en Garantía:** Crear un producto o variante "fantasma" que se agregue automáticamente al carrito cuando detecte un artículo de renta, cubriendo el depósito.
*   **3.3. Contrato Digital en Carrito:** Añadir un Checkbox nativo obligatorio en el carrito (`cart.liquid`) que guarde la firma de los Términos de Renta como un atributo del carrito para protección legal.

### 4. Fase 4: Portal de Socios y Mayoreo B2B (Sin Apps)
Evitaremos apps de "Wholesale" usando validaciones de etiquetas (Customer Tags).

*   **4.1. Portal de Acceso y Precios Bloqueados (Gatekeeper):** Crear un template de colección (`collection.b2b.liquid`) y lógica en productos que condicione: `{% if customer.tags contains 'B2B' %}`. Si no están logueados con el tag, ven precios de retail o la vista se bloquea mandándolos al login.
*   **4.2. Formularios de Registro Personalizados:** Desarrollar una landing page (`page.registro-b2b.liquid`) con un formulario nativo que solicite datos corporativos y añada un tag "B2B_Pendiente" para revisión manual del administrador.
*   **4.3. Listas de Precios por Volumen:** Modificar los templates de producto para calcular y mostrar tablas de descuentos progresivos basados en cantidad de piezas en el carrito mediante *Shopify Functions* o Scripts nativos de descuento automático.

### 5. Fase 5: Experiencia de Usuario (UI/UX) y Conversión
*   **5.1. Fichas Técnicas Avanzadas:** Desplegar la composición, guía de tallas y origen usando bloques dinámicos dentro de la PDP, haciendo que la experiencia de lectura sea limpia y "Premium".
*   **5.2. Image Swap on Hover:** Activar cambio de imagen en Product Cards en los PLPs.
*   **5.3. Botón de Conversión a WhatsApp:** Botón flotante dinámico que lea el SKU actual e inicie una conversación preescrita para ventas consultivas.

### 6. Fase 6: QA, Rendimiento y Despliegue
*   **6.1. Benchmarking de Velocidad:** Auditoría en PageSpeed Insights. Objetivo: LCP menor a 1.5s y mantener puntajes altos en móviles, garantizando que el JS del calendario de rentas no bloquee la carga.
*   **6.2. UAT (User Acceptance Testing):** Pruebas de estrés para: Flujo de checkout B2C, validación de fechas cruzadas en Rentas, y login de cuenta Mayoreo.
*   **6.3. Merge & Deploy:** Fusión a rama principal y lanzamiento a producción del tema vitaminado.

---

## 📝 Notas Estratégicas
*   **Sostenibilidad:** Al eliminar apps de Rentas, Mayoristas y Filtros, no solo se ahorrará en pagos mensuales, sino que el tiempo de carga total del sitio mejorará drásticamente.
*   **Escalabilidad:** Toda la arquitectura de Metafields está pensada para integrarse sin problemas si en el futuro migran a Shopify Plus.
