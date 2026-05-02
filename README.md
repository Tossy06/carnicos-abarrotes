# Cárnicos & Abarrotes

Sitio web estático para una empresa distribuidora de cárnicos y abarrotes ubicada en Bogotá, Colombia. Desarrollado como taller práctico de control de versiones con Git y GitHub.

## Demo en vivo

**[tossy06.github.io/carnicos-abarrotes](https://tossy06.github.io/carnicos-abarrotes/)**

## Descripción

Sitio de tres páginas que presenta los productos, valores y datos de contacto de la empresa. Diseño moderno y responsivo con animaciones CSS, secciones parallax y Bootstrap 5.

## Tecnologías

| Tecnología | Uso |
|---|---|
| HTML5 + CSS3 | Estructura y estilos |
| Bootstrap 5.3 | Grid, componentes y utilidades |
| Bootstrap Icons 1.11 | Iconografía |
| Google Fonts — Inter | Tipografía |
| Git + GitHub CLI | Control de versiones |
| GitHub Pages | Despliegue |

## Estructura del proyecto

```
carnicos-abarrotes/
├── index.html          # Inicio — hero, valores, galería
├── productos.html      # Catálogo de cárnicos y abarrotes
├── contacto.html       # Hero con imagen, info y formulario
├── css/
│   └── style.css       # Estilos personalizados
├── img/                # Imágenes locales
├── README.md           # Este archivo
└── documentacion.md    # Comandos Git y flujo de trabajo
```

## Páginas

| Página | Contenido |
|---|---|
| `index.html` | Hero centrado con estadísticas, sección de valores, banner parallax y galería de imagen de marca |
| `productos.html` | Catálogo dividido en cárnicos y abarrotes, con badges de disponibilidad y banner parallax central |
| `contacto.html` | Hero con imagen de fondo sticky, barra de datos de contacto horizontal y formulario centrado |

## Ejecutar localmente

```bash
git clone https://github.com/Tossy06/carnicos-abarrotes.git
cd carnicos-abarrotes
```

Abrir `index.html` directamente en el navegador. No requiere servidor ni instalación de dependencias — Bootstrap e Inter se cargan desde CDN.

## Flujo de ramas

```
main
├── feature/catalogo  →  PR #1 — Catálogo de productos
├── feature/contacto  →  PR #2 — Página de contacto
└── feature/galeria   →  PR #3 — Galería e imagen de marca
```

Cada funcionalidad se desarrolló en una rama independiente y se integró a `main` mediante Pull Request.  
Ver [`documentacion.md`](./documentacion.md) para el detalle completo de comandos.

## Publicación

El sitio está publicado en **GitHub Pages** desde la rama `main`, carpeta raíz.  
URL: `https://tossy06.github.io/carnicos-abarrotes/`

---

Desarrollado por **Tossy06** — Taller práctico de GitHub.
