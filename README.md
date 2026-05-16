# Copal Inc — Website

Sitio web corporativo de **Copal Inc**, una empresa de desarrollo de software a medida con sede en Ciudad de México. Construido como un único archivo HTML estático, desplegado en GitHub Pages con dominio personalizado.

---

## Tecnologías

| Herramienta | Uso |
|---|---|
| HTML5 + CSS3 | Estructura y estilos base |
| [Tailwind CSS](https://tailwindcss.com) (CDN) | Utilidades de diseño y layout |
| [Alpine.js](https://alpinejs.dev) | Navegación móvil y estado del formulario |
| [AOS](https://michaelosajetz.com/aos/) | Animaciones al hacer scroll |
| [FormSubmit.co](https://formsubmit.co) | Envío del formulario de contacto sin backend |
| Google Fonts | Playfair Display + Inter |
| GitHub Pages | Hosting estático |

---

## Estructura del proyecto

```
website/
├── index.html        # Todo el sitio (HTML + CSS inline + JS)
├── copal_logo.png    # Logo y favicon
├── CNAME             # Dominio personalizado: copalinc.com
└── README.md         # Este archivo
```

---

## Secciones del sitio

1. **Hero** — Headline principal con árbol SVG animado y hojas cayendo
2. **Servicios** — 5 tarjetas de servicios (Software, UX/UI, Cloud, Soporte, Ciberseguridad)
3. **Por qué Copal** — 4 diferenciadores con contadores animados
4. **Proceso** — Timeline de 5 pasos con líneas animadas al scroll
5. **Equipo** — Tarjetas del equipo con placeholders para futuros miembros
6. **Contacto** — Formulario AJAX + datos de contacto

---

## Bilingüe (ES / EN)

El sitio detecta automáticamente el idioma del navegador del visitante:

- **Español** → visitantes con cualquier idioma que no sea inglés (defecto)
- **Inglés** → visitantes con `navigator.language` que empiece con `en`

La preferencia se guarda en `localStorage` con la clave `copal-lang`. El usuario también puede cambiar el idioma manualmente con el toggle **ES | EN** en la barra de navegación.

### Cómo agregar/editar traducciones

Todas las traducciones están en el objeto `i18n` al inicio del `<head>` en `index.html`:

```javascript
const i18n = {
  es: {
    nav_services: 'Servicios',
    hero_h1: 'Del concepto<br>al producto,...',
    // ...
  },
  en: {
    nav_services: 'Services',
    hero_h1: 'From concept<br>to product,...',
    // ...
  }
};
```

En el HTML, los elementos usan atributos `data-i18n`:

| Atributo | Uso |
|---|---|
| `data-i18n="key"` | Actualiza `textContent` del elemento |
| `data-i18n-html="key"` | Actualiza `innerHTML` (para contenido con etiquetas HTML) |
| `data-i18n-placeholder="key"` | Actualiza el `placeholder` de inputs |

---

## Formulario de contacto

El formulario usa **[FormSubmit.co](https://formsubmit.co)**, un servicio gratuito que reenvía submissions a tu email sin necesidad de backend ni registro previo.

### Configuración (solo una vez)

1. La primera vez que alguien envíe el formulario, FormSubmit enviará un **correo de activación** a `contacto@copalinc.com`
2. Haz clic en el link de activación en ese correo
3. A partir de ahí, todos los mensajes del formulario llegarán automáticamente

### Cambiar el email de destino

Busca en `index.html`:
```html
action="https://formsubmit.co/ajax/contacto@copalinc.com"
```
Reemplaza `contacto@gmail.com` con el email deseado.

### Campos del formulario

| Campo | Nombre | Requerido |
|---|---|---|
| Nombre | `nombre` | Sí |
| Empresa | `empresa` | No |
| Email | `email` | Sí |
| Servicio | `servicio` | No |
| Mensaje | `mensaje` | Sí |

---

## Desarrollo local

No requiere build ni dependencias. Basta con abrir `index.html` en un navegador, o servir con cualquier servidor HTTP estático:

```bash
# Con Python
python3 -m http.server 8000

# Con Node.js (npx)
npx serve .

# Con VS Code: extensión Live Server
```

---

## Despliegue (GitHub Pages)

El sitio se despliega automáticamente en cada push a la rama `main`.

- **Repositorio:** `github.com/[usuario]/website`
- **Dominio:** `copalinc.com` (configurado en `CNAME`)
- **Rama de despliegue:** `main` (raíz del repositorio)

### Configurar dominio personalizado

1. El archivo `CNAME` ya contiene `copalinc.com`
2. En el proveedor de DNS, apunta los registros A a las IPs de GitHub Pages:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
3. En la configuración del repositorio → Pages → Custom domain → ingresa `copalinc.com`

---

## Actualizar contenido

### Agregar un miembro del equipo

1. Localiza la sección `<!-- ===== TEAM ===== -->` en `index.html`
2. Reemplaza uno de los bloques `team-placeholder` con una `team-card` real:

```html
<div class="team-card rounded-2xl p-7" data-aos="fade-up">
  <img src="URL_FOTO" alt="Nombre Apellido"
       class="w-16 h-16 rounded-full object-cover border-2 border-jade/30 mb-4">
  <h3 class="font-serif text-xl font-bold text-ivory mb-0.5">Nombre Apellido</h3>
  <p class="text-jade text-xs font-semibold tracking-wide mb-3">Rol</p>
  <p class="text-mid-gray text-sm leading-relaxed mb-5">Bio corta del miembro.</p>
  <!-- social links opcionales -->
</div>
```

### Modificar servicios

Localiza `<!-- ===== SERVICES ===== -->` y edita el `data-i18n` key correspondiente en el objeto `i18n` para reflejar el cambio en ambos idiomas.

---

## Contacto

- **Email:** contacto@gmail.com
- **Instagram:** [@copal.inc](https://instagram.com/copal.inc)
- **LinkedIn:** [Eithan Treviño](https://linkedin.com/in/eithan-trevino)
