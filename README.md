# Demo Comercial — VETCARE (Clínica Veterinaria)

Demo de **sitio web profesional** para una clínica veterinaria, creada para
mostrar a posibles clientes qué puede esperar de un trabajo real de diseño web.

> **Aviso importante**
> Este proyecto es una **demostración**. **VETCARE es un negocio ficticio**
> creado por Kovatek únicamente como ejemplo de diseño.
> Los servicios, horarios y ubicación son **contenido de ejemplo** y están
> marcados como tales en la página. No se han inventado años de experiencia,
> certificaciones, reconocimientos, dirección real, reseñas ni redes sociales.
> **Ningún dato de esta página corresponde a una clínica real.**

---

## 1. Qué es el proyecto

Una página web de una sola página (*landing page*) con diseño premium, pensada para
clínicas veterinarias que hoy no tienen presencia en internet.

**Incluye:**

| Sección | Descripción |
|---|---|
| Navbar sticky | Logo, 5 enlaces de navegación, botón **Agendar por WhatsApp** y menú móvil |
| Hero | Imagen de fondo, título, descripción, dos llamados a la acción y leyenda de demo |
| Servicios | 6 tarjetas con icono, nombre y descripción (contenido de ejemplo) |
| Nosotros | Dos columnas: imagen + texto con 3 puntos sobre la forma de trabajar |
| Beneficios | 4 bloques numerados (01–04) |
| Instalaciones | Cuadrícula responsive de 6 imágenes con *lightbox* |
| Horarios y ubicación | Tabla de horarios + espacio reservado para Google Maps |
| Contacto | Categoría, servicios, ubicación, teléfono y horarios, con CTA de WhatsApp |
| Kovatek | Sección de conversión: propuesta de valor y servicios independientes |
| Footer | Marca, enlaces, contacto, crédito de demo y aviso legal |

**Tecnologías usadas** (solo frontend, sin backend ni base de datos):

* HTML5 semántico
* Tailwind CSS (CDN)
* JavaScript vanilla
* Google Fonts (Sora + Inter)
* Imágenes de demostración servidas desde Unsplash
* Vercel Web Analytics

**No se usa:** React, Angular, Vue, TypeScript, Node.js, npm, Firebase, API propias
ni ningún sistema de autenticación.

---

## 2. Cómo abrirlo

No requiere instalación, compilación ni servidor.

1. Abre la carpeta `demo-veterinaria`
2. Haz doble clic en **`index.html`**
3. Se abrirá en tu navegador

También puedes usar un servidor local opcional (si quieres ver el comportamiento
exacto de un hosting):

```bash
# con Python
python -m http.server 8000

# o con Node.js
npx serve .
```

Luego visita `http://localhost:8000`.

> La página carga Tailwind, las tipografías y las imágenes desde CDN, por lo que
> **necesita conexión a internet** para verse completa. El resto del código
> funciona siempre de forma local.

---

## 3. Dónde se cambia cada cosa

**Casi todo se cambia en un solo archivo:** `js/main.js`, en el **bloque 1
(Configuración central del negocio)**.

```js
const business = {
  name: 'VETCARE',
  brand: 'VETCARE',
  brandTagline: 'Clínica Veterinaria',
  category: 'Clínica Veterinaria',
  // ...
};
```

El resto del archivo genera la página a partir de esos datos.

| Qué cambiar | Dónde |
|---|---|
| Nombre y marca | `js/main.js` → `business.name`, `business.brand`, `business.brandTagline` |
| Servicios | `js/main.js` → array `services` |
| Horario de atención | `js/main.js` → array `schedule` |
| Puntos de "Nosotros" | `js/main.js` → `aboutList` |
| Ubicación y dirección | `js/main.js` → `business.city`, `business.address` |
| Teléfono | `js/main.js` → `business.phone`, `business.phoneDisplay` |
| Imágenes | `js/main.js` → objeto `images` |
| Google Maps | `js/main.js` → `business.mapsUrl` |
| Redes sociales | `js/main.js` → `business.instagramUrl`, etc. |
| Colores | `index.html` → `tailwind.config` **y** las variables de `<style>` |
| Título y descripción SEO | `js/main.js` → `business.seoTitle`, `business.seoDescription` |
| Autoría del sitio (`<meta author>`) | `js/main.js` → `business.author` |

> Los textos que **no** debes olvidar al reutilizar la plantilla:
> el `<h1>` del hero, los `<h2>` de cada sección y el mensaje de WhatsApp.
> Esos tres viven directamente en `index.html`.

---

## 4. Cómo cambiar el teléfono

**Archivo:** `js/main.js` → objeto `business`

```js
phone: '521234567890',          // solo dígitos, para el enlace tel:
phoneDisplay: '212 345 6789',  // con espacios, como se muestra
```

En la demo ambos campos están **vacíos a propósito** y se muestra en su lugar
un marcador visible (`00 0000 0000 (ejemplo)`).

> **Importante:** el teléfono **nunca** debe derivarse del número de WhatsApp
> de Kovatek, o el número comercial aparecería como si fuera de la clínica.
> Al rellenar `phone`, el marcador de ejemplo desaparece automáticamente y
> queda una sola fila de teléfono.

---

## 5. Cómo cambiar WhatsApp

**Un solo lugar.** El número está centralizado en `js/main.js`:

```js
const whatsappNumber = '5219612165495';
```

Este valor alimenta `business.whatsapp` y se usa en `openWhatsApp()`, que está
conectada a **todos** los botones con el atributo `data-whatsapp`.

> En esta demo el número es el **canal comercial de Kovatek**, no el contacto de
> la marca ficticia VETCARE. Todos los botones de la página apuntan ahí.

**Formato:** solo números, con clave de país y sin `+`, espacios ni guiones.
Ejemplos:

| País | Valor |
|---|---|
| México | `521234567890` |
| España | `34600111222` |
| Colombia | `573001234567` |

**Mensaje inicial** (se puede personalizar):

```js
whatsappMessage: 'Hola, me gustaría solicitar información sobre sus servicios.',
```

**Agregar un botón de WhatsApp nuevo** — no necesitas JavaScript adicional,
solo agrega el atributo en cualquier elemento:

```html
<button type="button" data-whatsapp>Agendar</button>
```

---

## 6. Cómo cambiar los servicios

**Archivo:** `js/main.js` → array `services`

```js
const services = [
  {
    id: 'consulta-general',
    name: 'Consulta general',
    description: 'Revisión clínica completa.',
    icon: 'stethoscope',   // clave de ICONS
    price: null,           // número para mostrarlo, o null para «Consultar»
    currency: 'MXN',
    duration: ''           // opcional, por ejemplo '45 min'
  }
];
```

Las tarjetas se generan automáticamente: **añadir, quitar o reordenar
servicios solo requiere editar este array.**

**Iconos disponibles** (`ICONS` en `js/main.js`):

`paw`, `stethoscope`, `syringe`, `bug`, `shield`, `sparkles`, `flask`,
`map`, `phone`, `clock`, `arrow`, `instagram`, `facebook`, `tiktok`.

**Para poner precios reales**, cambia `price: null` por el número:

```js
price: 350,   // se muestra como «$350 MXN»
```

> Cuando los precios sean reales, revisa también la nota al pie de la sección
> de servicios, que dice que son datos de ejemplo.

---

## 7. Cómo cambiar el horario

**Archivo:** `js/main.js` → array `schedule`

```js
const schedule = [
  { day: 'Lunes a viernes', time: '9:00 – 18:00' },
  { day: 'Sábado', time: '9:00 – 14:00' },
  { day: 'Domingo', time: 'Cerrado' }
];
```

> En esta demo los horarios son ilustrativos y la página lo indica de forma
> visible. Si el día aparece como **Cerrado**, el texto se muestra atenuado
> automáticamente.

---

## 8. Cómo cambiar las imágenes

Todas las imágenes están **centralizadas** en `js/main.js`, dentro del objeto `images`,
y se asignan a la página mediante atributos `data-img` en `index.html`:

| Atributo | Dónde se usa |
|---|---|
| `data-img="hero"` | Fondo de la sección Hero |
| `data-img="about"` | Imagen de la sección Nosotros |
| `data-img="gallery.0"` … `gallery.5` | Las 6 imágenes de la galería |

**Recomendación:** al usar imágenes reales, guárdalas en `assets/` y usa rutas
locales (más rápido y sin depender de internet):

```js
hero: 'assets/hero.jpg',
about: 'assets/nosotros.jpg',
gallery: [
  { src: 'assets/galeria-1.jpg', alt: 'Descripción real' }
  // ...
]
```

> Cada imagen de la galería necesita su campo `alt`: se usa en la miniatura y en
> la vista ampliada.

Consulta `assets/README.md` para medidas recomendadas, formatos y nombres.

---

## 9. Cómo cambiar los colores

La paleta está definida en **dos lugares**. Cambia ambos.

**A) Configuración de Tailwind** — `index.html`, dentro de `<script>`:

```js
tailwind.config = {
  theme: {
    extend: {
      colors: {
        ink: '#072A38',        // azul petróleo profundo (fondo oscuro / texto)
        lagoon: '#0C3D4F',     // azul petróleo medio (fondo oscuro secundario)
        mist: '#F5FAFB',       // fondo claro
        sea: '#2FB89A',        // esmeralda suave (acento sobre oscuro)
        'sea-deep': '#0F7A63', // esmeralda legible sobre claro
        'sea-soft': '#BEE9DE'  // esmeralda clara (hover)
      },
      fontFamily: {
        display: ['Sora', 'sans-serif'],  // títulos
        body: ['Inter', 'sans-serif']     // texto
      }
    }
  }
};
```

**B) Variables CSS** — `index.html`, dentro de `<style>` (se usan en el navbar,
el lightbox, las animaciones y el hover del menú):

```css
:root {
  --c-ink: #072A38;
  --c-lagoon: #0C3D4F;
  --c-mist: #F5FAFB;
  --c-sea: #2FB89A;
  --c-sea-deep: #0F7A63;
}
```

**Notas importantes:**

* `sea` (`#2FB89A`) se usa sobre fondos oscuros: botones, iconos, subrayados.
  Sobre fondos claros el esmeralda no cumple contraste, por eso existe
  `sea-deep`, que es el mismo color más oscuro.
* Si cambias el color de acento, verifica el contraste:
  **mínimo 4.5:1** para texto normal y **3:1** para texto grande.
* Para cambiar las tipografías, edita también el `<link>` de Google Fonts
  en `<head>` y las dos listas en `tailwind.config`.

---

## Bonus: otros datos personalizables

### Mapa de Google Maps

`js/main.js` → objeto `business`:

```js
mapsUrl: '',
```

Pega ahí el enlace de Google Maps y el botón **"Consultar ubicación"** abrirá la
ubicación real. Mientras esté vacío, muestra un aviso indicando que la ubicación
es un dato de ejemplo.

Para embeber el mapa directamente, reemplaza el bloque con el mapa
(la tarjeta `map-grid` de la sección `#horarios`) por:

```html
<iframe
  src="https://www.google.com/maps/embed?pb=..."
  class="h-full min-h-[18rem] w-full rounded-2xl border-0"
  loading="lazy"
  referrerpolicy="no-referrer-when-downgrade"
  title="Ubicación de la clínica"></iframe>
```

### Redes sociales

`js/main.js` → `business.instagramUrl`, `business.facebookUrl`, `business.tiktokUrl`.

Están **vacías a propósito** (no se inventan redes sociales de un negocio
ficticio). Al rellenar una URL, su icono aparece automáticamente en el contacto
y en el pie de página. Si las tres quedan vacías, el bloque se oculta.

### Etiquetas de "Demo"

Para que la página deje de ser una demo, elimina o reescribe estos elementos:

| Ubicación | Texto |
|---|---|
| Hero | "Demostración ficticia desarrollada por Kovatek. VETCARE no es una clínica real." |
| Hero | La barra de ubicación y horarios de ejemplo |
| Servicios | La nota "Servicios de ejemplo para esta demostración..." |
| Beneficios | "Mensajes de ejemplo para una clínica ficticia..." |
| Instalaciones | "Imágenes de referencia. En un proyecto real se sustituyen..." |
| Horarios | "Los horarios mostrados son únicamente ilustrativos." |
| Contacto | El teléfono `00 0000 0000 (ejemplo)` |
| Contacto | "Ubicación de ejemplo" |
| Footer | "Demo desarrollada por Kovatek" |
| Footer | El aviso `data-render="demoNote"` |
| `index.html` head | `<meta name="robots" content="noindex, nofollow">` |

> Quita `noindex, nofollow` antes de publicar el sitio real, o no aparecerá
> en buscadores.

### Vercel Web Analytics

Ya está instalado en el `<head>` de `index.html`:

```html
<script>
  window.va = window.va || function () {
    (window.vaq = window.vaq || []).push(arguments);
  };
</script>
<script defer src="/_vercel/insights/script.js"></script>
```

Funciona automáticamente al desplegar en Vercel. En local simplemente no envía
datos. Si prefieres no usarlo, elimina ambos `<script>`.

---

## Estructura del proyecto

```
demo-veterinaria/
│
├── index.html      # Estructura y contenido de la página
├── js/
│   └── main.js     # Configuración + toda la lógica
├── assets/
│   └── README.md   # Guía de imágenes
└── README.md       # Este archivo
```

### Resumen de `js/main.js`

| Sección | Contenido |
|---|---|
| 1 | Configuración central (`business`, `services`, `schedule`, `images`) |
| 2 | Utilidades de formato |
| 3 | Iconos SVG |
| 4 | Render de contenido dinámico |
| 5 | Imágenes |
| 6 | SEO dinámico |
| 7 | WhatsApp (`openWhatsApp`) |
| 8 | Menú móvil |
| 9 | Scroll suave |
| 10 | Navbar al hacer scroll |
| 11 | Lightbox de galería |
| 12 | Botón volver arriba |
| 13 | Animaciones al aparecer las secciones |
| 14 | Google Maps (placeholder) |
| 15 | Inicialización |

Todo está dentro de una función anónima (IIFE) en modo estricto, sin variables
globales salvo `window.vetcareSite`, que expone la configuración para facilitar
la depuración desde la consola del navegador.

**Regla de oro:** cualquier campo vacío (`''` o `null`) oculta automáticamente
su bloque: dirección, mapa, precios, teléfono, logotipo y redes sociales.

---

## Funcionalidades incluidas

* Menú móvil con animación y cierre automático
* Scroll suave con compensación del navbar fijo
* Navbar que cambia de opacidad al hacer scroll
* Galería con *lightbox* (ESC, clic fuera y botón para cerrar)
* Botón de volver arriba
* Animaciones de entrada con `IntersectionObserver`
* Envío de mensajes por WhatsApp con un solo clic
* Respeto a `prefers-reduced-motion` (accesibilidad)
* Enlace "Saltar al contenido" para navegación por teclado
* Marca `noindex, nofollow` para que los buscadores no la indexen

---

## Compatibilidad

Verificado en Chrome (headless) simulando anchos de **320, 375, 430, 768, 1024 y
1440 px**:

* Sin scroll horizontal en ningún ancho (`scrollWidth` igual al ancho del viewport).
* Menú hamburguesa por debajo de 1024 px; navegación horizontal desde 1024 px.
* Grilla de servicios en 1 → 2 → 3 columnas; galería en 1 → 2 → 3 columnas.
* Menú móvil, lightbox y botones de WhatsApp funcionando en todos los anchos.
* Ningún enlace `tel:` apunta al número comercial de Kovatek.

## Licencia y uso

Demo comercial creada por Kovatek para presentación de trabajos.
Las fotografías de Unsplash se usan únicamente con fines ilustrativos y
**no representan el negocio mostrado**. Sustitúyelas por fotografías propias
antes de entregar el sitio a un cliente.
