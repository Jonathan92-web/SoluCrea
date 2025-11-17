# SoluCrea - Instrucciones para Agentes de IA

## Descripción General del Proyecto

**SoluCrea DIGITAL** es una landing page/sitio web corporativo para una agencia full-service de marketing digital. El proyecto es un **sitio estático HTML5** sin framework backend, enfocado en conversión (CTAs) y animaciones visuales atractivas.

### Stack Tecnológico
- **HTML5** (`index.html`) - estructura semántica única
- **CSS3** (`styles/main.css`) - utilidad + componentes personalizados
- **Vanilla JavaScript** (`js/main.js`) - interactividad mínima y específica
- **Tailwind CSS** - framework de utilidad cargado vía CDN
- **AOS (Animate On Scroll)** - librería de animaciones al scroll, cargada desde CDN

## Arquitectura y Componentes Clave

### Estructura de Secciones HTML
El sitio sigue un patrón de una sola página (one-pager) con secciones ancladas:

1. **Header Sticky** (`<header>`)
   - Navegación desktop (oculta en móvil)
   - Menú hamburguesa móvil (id: `mobile-menu-button`)
   - CTA principal "Cotiza tu Proyecto"
   - Usa `backdrop-filter` para efecto glassmorphism

2. **Hero Section** (`.bg-dark-black`)
   - Fondo oscuro con gradientes abstractos (blobs animados)
   - Grid 2 columnas desktop
   - Animaciones AOS: `fade-right`, `fade-up`, `fade-left`

3. **Services Section** (`#servicios`)
   - Grid 2x2 de tarjetas de servicios
   - Interactividad: `hover:-translate-y-2` + cambio de color en iconos
   - 4 pilares: Marketing Digital, Producción Audiovisual, Desarrollo Web, Community Manager

4. **Testimonials Section** (`#casos`)
   - Grid simple 1x3 de testimonios
   - Minimal, sin lógica JavaScript

5. **Contact Form Section** (`#contacto`)
   - Grid 5 columnas: 2 col info (lado oscuro), 3 col formulario
   - Selector de servicio (`<select>`)
   - Alert placeholder: `alert('¡Mensaje Enviado! (Demo)')`

6. **Footer** (`<footer>`)
   - Grid 4 columnas con links
   - Redes sociales placeholder (IG, FB, LI)

### Marca Visual
- **Color Primario**: `#C40233` (rojo) → clase `.text-primary-red`, `.cta-gradient`
- **Color Secundario**: `#1A202C` (gris oscuro) → clase `.bg-dark-black`, `.text-dark-black`
- **Fuente**: Inter (Google Fonts, pesos: 400, 500, 600, 700, 900)
- **Espaciado**: max-width `7xl` (1280px), padding responsivo `px-4 sm:px-6 lg:px-8`

## Convenciones y Patrones

### Naming Conventions
- **Clases Tailwind**: Preferencia por utilidades directas + extensión custom en `main.css`
- **Clases Custom**: `.cta-gradient`, `.icon-service`, `.mobile-link`, `.shadow-red`
- **Data Attributes**: `data-aos` (animaciones), `data-contact-form` (formulario)
- **IDs**: CamelCase simplificado: `mobile-menu-button`, `mobile-menu`, `contact-form`

### Animaciones (AOS)
Patrón estándar en elementos clave:
```html
<div data-aos="fade-up" data-aos-delay="100" data-aos-duration="800">
```
- **Delays**: Incrementos de 100-200ms para efecto en cascada
- **Duration**: Típicamente 800-1200ms
- **Once**: Configurado en script (animaciones ocurren una sola vez)
- Tipos usados: `fade-up`, `fade-right`, `fade-left`, `fade-down`, `zoom-in`, `zoom-in-up`

### Efectos CSS Personalizados
- `.cta-gradient` - gradiente rojo animado en hover
- `.shadow-red` - sombra roja para CTAs
- `.pulse-glow` - efecto de pulso (Tailwind: `animate-pulse`)
- `.icon-service` - contenedores circulares con fondo claro

## Flujos de Interacción Implementados

### 1. Menú Móvil
**Archivo**: `js/main.js` (líneas 1-17)

Patrón de toggle simple:
```javascript
mobileMenuButton.addEventListener('click', () => {
    mobileMenu.classList.toggle('hidden');
});
mobileLinks.forEach(link => {
    link.addEventListener('click', () => {
        mobileMenu.classList.add('hidden'); // Cerrar al hacer click
    });
});
```

**Clases clave**:
- `.hidden` (Tailwind) para ocultar/mostrar
- Selector: `#mobile-menu-button`, `#mobile-menu`, `.mobile-link`

### 2. Formulario de Contacto
**Archivo**: `js/main.js` (líneas 19-25)

Currently: Placeholder con `alert()`. Estructura para extensión futura:
```javascript
const contactForm = document.querySelector('[data-contact-form]');
if (contactForm) {
    contactForm.addEventListener('submit', (e) => {
        e.preventDefault();
        // TODO: Integración con backend (email, CRM, webhook)
    });
}
```

**Elementos del formulario**:
- Nombre, Empresa (grid 2 col)
- Email, Servicio (full width)
- Mensaje (textarea)
- Botón submit con clase `.cta-gradient`

## Integración de Dependencias Externas

### CDN Cargadas
1. **Tailwind CSS** v3 (vía script, con config inline)
2. **AOS** v2.3.1 - CSS + JS
3. **Google Fonts** - Inter (5 pesos)

### Tailwind Config Personalizado
```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        'dark-black': '#1A202C',
        'primary-red': '#C40233'
      }
    }
  }
}
```

### Configuración AOS
```javascript
AOS.init({
    once: true,
    offset: 100,
    easing: 'ease-in-out-sine'
});
```

## Patrones de Desarrollo

### Agregar Nuevas Secciones
1. Crear bloque `<section id="nombre">` con clase `py-24 md:py-36`
2. Wrapper interior: `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8`
3. Aplicar `data-aos` a elementos clave
4. Usar grid Tailwind: `grid-cols-1 md:grid-cols-2 lg:grid-cols-4`
5. Incluir en footer links si es relevante

### Modificar Estilo Global
- **Colores**: Extensión en tailwind config (dentro de `<script>` en HTML)
- **Tipografía**: Estilos en `main.css` (ya es Inter + line-height)
- **Componentes**: Clases custom en `main.css` (ej: `.cta-gradient`, `.icon-service`)

### Responsive Design
- **Breakpoints Tailwind**: `sm` (640px), `md` (768px), `lg` (1024px)
- **Patrón común**: `hidden md:flex`, `grid-cols-1 md:grid-cols-2`
- **Tipografía**: `text-2xl md:text-4xl` (escala según pantalla)

## Notas Importantes

- **Sin Build Step**: Proyecto estático, sin webpack/bundler
- **Sin Backend Actual**: Formulario actualmente es demo (`alert()`)
- **Branch Actual**: `animaciones-2` (en Git, rama de trabajo para animaciones)
- **Rutas Relativas**: Todos los assets usan rutas relativas (`styles/main.css`, `js/main.js`)
- **URLs Hardcoded**: WhatsApp (`https://wa.me/573189776429`), email contacto estático

## Tareas Comunes para Agentes IA

### Agregar Animación a Elemento
1. Identificar selector (clase/ID)
2. Añadir atributo `data-aos="tipo-animacion"`
3. Opcionalmente: `data-aos-delay="100"` y `data-aos-duration="800"`
4. No requiere cambio en JS (AOS maneja automáticamente)

### Cambiar Colores de Marca
1. Actualizar inline Tailwind config (líneas 6-14 en `index.html`)
2. Actualizar variables en `main.css` (comentarios referenciados)
3. Buscar hardcoded hex (`#C40233`, `#1A202C`) y reemplazar globalmente

### Integrar Formulario Real
1. Reemplazar `alert()` por fetch a endpoint
2. Validación client-side: agregar atributos `required`, `type="email"`, etc.
3. Manejo de error/éxito (mostrar mensaje sin salir de página)
4. Considerar: reCAPTCHA, rate limiting

### Agregar Nueva Sección de Servicios
1. Duplicar tarjeta en grid 2x2 → ajustar a grid 2x3 si es necesario
2. Cambiar icono SVG (Lucide icons, mismo patrón)
3. Actualizar descripción y lista de características
4. Agregar delay AOS incremental (100, 200, 300, 400, 500...)

---

**Última Actualización**: 16 nov 2025  
**Rama Activa**: animaciones-2
