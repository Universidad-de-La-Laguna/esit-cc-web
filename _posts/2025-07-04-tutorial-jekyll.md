---
layout: post
title: "Tutorial Jekyll"
date: 2025-07-04
categories: blog
---

# Guía completa de Jekyll - De cero a experto

## Índice
1. [¿Qué es Jekyll?](#qué-es-jekyll)
2. [Instalación y configuración](#instalación-y-configuración)
3. [Estructura de archivos](#estructura-de-archivos)
4. [Configuración básica](#configuración-básica)
5. [Creando contenido](#creando-contenido)
6. [Temas y personalización](#temas-y-personalización)
7. [Plugins y extensiones](#plugins-y-extensiones)
8. [Publicación y deployment](#publicación-y-deployment)
9. [Consejos avanzados](#consejos-avanzados)

---

## ¿Qué es Jekyll?

Jekyll es un generador de sitios web estáticos de código abierto escrito en Ruby. Se utiliza principalmente para crear blogs y sitios web simples que no requieren una base de datos.

### Características principales:
- **Velocidad**: Los sitios estáticos cargan muy rápido
- **Seguridad**: No hay base de datos que pueda ser comprometida
- **Simplicidad**: Fácil de mantener y actualizar
- **Control de versiones**: Puedes usar Git para gestionar tu contenido
- **Hosting gratuito**: Compatible con GitHub Pages

### Casos de uso comunes:
- Blogs personales
- Documentación de proyectos
- Sitios web de portfolios
- Páginas de landing simples
- Sitios web académicos

---

## Instalación y configuración

### Prerrequisitos
```bash
# Verificar instalación
ruby --version    # Versión 2.7 o superior
gem --version
bundler --version

# Instalar Jekyll
gem install jekyll bundler
```

### Crear tu primer sitio
```bash
# Crear nuevo sitio
jekyll new mi-blog
cd mi-blog

# Instalar dependencias
bundle install

# Ejecutar servidor local
bundle exec jekyll serve
```

---

## Estructura de archivos

### Estructura completa de un sitio Jekyll:

```bash
mi-sitio-jekyll/
├── _config.yml                 # Configuración principal
├── _config_development.yml     # Configuración para desarrollo
├── Gemfile                     # Dependencias de Ruby
├── Gemfile.lock               # Versiones específicas
├── .gitignore                 # Archivos a ignorar en Git
├── README.md                  # Documentación del proyecto
├── index.md                   # Página principal
├── 404.md                     # Página de error 404
├── about.md                   # Página "Acerca de"
├── contact.md                 # Página de contacto
│
├── _layouts/                  # Plantillas base
│   ├── default.html          # Layout principal
│   ├── post.html             # Layout para posts
│   ├── page.html             # Layout para páginas
│   └── home.html             # Layout para página principal
│
├── _includes/                 # Componentes reutilizables
│   ├── header.html           # Cabecera del sitio
│   ├── footer.html           # Pie de página
│   ├── nav.html              # Navegación
│   ├── head.html             # Meta tags y CSS
│   └── sidebar.html          # Barra lateral
│
├── _posts/                    # Entradas del blog
│   ├── 2024-01-01-mi-primer-post.md
│   ├── 2024-01-15-segundo-post.md
│   └── 2024-02-01-tercer-post.md
│
├── _drafts/                   # Borradores (no publicados)
│   ├── post-en-desarrollo.md
│   └── ideas-futuras.md
│
├── _data/                     # Archivos de datos
│   ├── navigation.yml        # Datos de navegación
│   ├── authors.yml           # Información de autores
│   └── social.yml            # Enlaces sociales
│
├── _sass/                     # Archivos Sass/SCSS
│   ├── _base.scss            # Estilos base
│   ├── _layout.scss          # Estilos de layout
│   ├── _syntax-highlighting.scss
│   └── _custom.scss          # Estilos personalizados
│
├── assets/                    # Recursos estáticos
│   ├── css/
│   │   └── main.scss         # Archivo principal de CSS
│   ├── js/
│   │   └── main.js           # JavaScript personalizado
│   ├── images/
│   │   ├── logo.png
│   │   ├── avatar.jpg
│   │   └── posts/            # Imágenes de posts
│   └── fonts/                # Fuentes personalizadas
│
└── _site/                     # Sitio generado (no subir a Git)
    ├── index.html
    ├── about/
    ├── assets/
    └── ...
```

### Carpetas que Jekyll entiende automáticamente:
- **`_posts/`** - Entradas del blog
- **`_drafts/`** - Borradores no publicados
- **`_layouts/`** - Plantillas base
- **`_includes/`** - Componentes reutilizables
- **`_data/`** - Archivos de datos
- **`_sass/`** - Archivos Sass/SCSS
- **`_site/`** - Sitio generado automáticamente

---

## Configuración básica

### `_config.yml` mínimo:
```yaml
title: Mi Blog
description: Una descripción de mi sitio
author: Tu Nombre
url: "https://tuusuario.github.io"
baseurl: ""

markdown: kramdown
highlighter: rouge
```

### `_config.yml` completo:
```yaml
# Información básica del sitio
title: Mi Blog Jekyll
description: Un blog personal sobre tecnología y desarrollo
author: Tu Nombre
email: tu@email.com

# URL del sitio
url: "https://tuusuario.github.io"
baseurl: ""

# Configuración de construcción
markdown: kramdown
highlighter: rouge
permalink: /:categories/:year/:month/:day/:title/

# Plugins básicos
plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-seo-tag

# Configuración de kramdown
kramdown:
  input: GFM
  hard_wrap: false
  syntax_highlighter: rouge

# Archivos a excluir
exclude:
  - README.md
  - Gemfile
  - Gemfile.lock
  - node_modules
  - vendor
  - .sass-cache
  - .jekyll-cache
  - .jekyll-metadata

# Variables personalizadas
social:
  twitter: tu_usuario
  github: tu_usuario
  linkedin: tu_usuario

# Configuración de zona horaria
timezone: Europe/Madrid

# Configuración por defecto
defaults:
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
      comments: true
  - scope:
      path: ""
      type: "pages"
    values:
      layout: "page"
```

### Kramdown (procesador de Markdown)
Kramdown es el procesador de Markdown que Jekyll usa por defecto. Convierte archivos `.md` en HTML con características especiales:

- **Atributos HTML**: `{: .mi-clase #mi-id}`
- **Tablas avanzadas** con alineación
- **Notas al pie**: `[^1]`
- **Bloques de código** con syntax highlighting
- **Matemáticas** (con MathJax)

### Permalinks
Los permalinks determinan las URLs de tus páginas:

```yaml
# Diferentes patrones
permalink: /:categories/:year/:month/:day/:title/  # /blog/2024/01/01/mi-post/
permalink: pretty                                   # /2024/01/01/mi-post/
permalink: /:categories/:title/                     # /blog/mi-post/
permalink: /:title/                                 # /mi-post/
```

---

## Creando contenido

### Estructura de un post:
```markdown
---
layout: post
title: "Mi primer post"
date: 2024-01-01 10:00:00 +0100
categories: blog tutorial
tags: jekyll markdown
author: Tu Nombre
---

# Mi contenido

Este es el contenido del post con **markdown**.

## Código de ejemplo
```javascript
function hola() {
  console.log("¡Hola Jekyll!");
}
```

> Esto es una cita importante

- Lista item 1
- Lista item 2
```

### Crear páginas:
```markdown
---
layout: page
title: Acerca de
permalink: /about/
---

Información sobre ti o tu sitio...
```

### Usar borradores:
```bash
# Crear borrador
touch _drafts/mi-borrador.md

# Mostrar borradores
bundle exec jekyll serve --drafts
```

---

## Temas y personalización

### Temas populares:
- **Minima** - Tema por defecto de Jekyll
- **Minimal Mistakes** - Muy completo y configurable
- **Beautiful Jekyll** - Fácil de usar
- **Academic** - Para sitios académicos

### Usar un tema:
```yaml
# En _config.yml
theme: minima

# O tema remoto (GitHub Pages)
remote_theme: "mmistakes/minimal-mistakes@4.24.0"
```

### Personalizar temas:
Puedes sobrescribir cualquier archivo del tema creando el mismo archivo en tu sitio:
```
tu-sitio/
├── _layouts/
│   └── post.html        # Sobrescribe el layout del tema
├── _includes/
│   └── header.html      # Sobrescribe el header del tema
└── _sass/
    └── custom.scss      # Estilos personalizados
```

---

## Plugins y extensiones

### Plugins que soporta GitHub Pages:
- **jekyll-feed** - Feed RSS automático
- **jekyll-sitemap** - Sitemap para SEO
- **jekyll-seo-tag** - Meta tags SEO
- **jekyll-paginate** - Paginación de posts
- **jemoji** - Soporte emojis :smile:

### Configuración de plugins:
```yaml
plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-seo-tag
  - jekyll-paginate
  - jemoji

paginate: 5
paginate_path: "/blog/page:num/"
```

### Limitaciones de GitHub Pages:
- Solo plugins oficiales
- No plugins de terceros
- No plugins personalizados

### Alternativas:
- **GitHub Actions** - Para usar cualquier plugin
- **Netlify/Vercel** - Soporte completo de plugins
- **Build local** - Construir y subir manualmente

---

## Publicación y deployment

### Proceso básico para GitHub Pages:

1. **Crear repositorio**: `tuusuario.github.io`
2. **Subir código**:
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/tuusuario/tuusuario.github.io.git
git push -u origin main
```
3. **Configurar GitHub Pages** en Settings → Pages
4. **Tu sitio estará en**: `https://tuusuario.github.io`

### Flujo de trabajo típico:
```bash
# 1. Crear nuevo post
touch _posts/2024-01-01-mi-nuevo-post.md

# 2. Escribir contenido
# 3. Probar localmente
bundle exec jekyll serve --drafts

# 4. Publicar
git add .
git commit -m "Nuevo post: Mi nuevo post"
git push origin main
```

### Otras opciones de hosting:
- **Netlify** - Automático desde GitHub
- **Vercel** - Deploy automático
- **Servidor propio** - Subir carpeta `_site/`

---

## Consejos avanzados

### Comandos útiles:
```bash
# Construir el sitio
bundle exec jekyll build

# Servidor local con live reload
bundle exec jekyll serve --livereload

# Limpiar archivos generados
bundle exec jekyll clean

# Actualizar dependencias
bundle update

# Mostrar versión
jekyll --version
```

### Optimización:
- **Usa cache** - Jekyll cachea automáticamente
- **Optimiza imágenes** - Comprime antes de subir
- **Minifica CSS/JS** - Usa plugins de minificación
- **CDN** - Para archivos estáticos grandes

### SEO básico:
```yaml
# En _config.yml
title: Tu Título
description: Descripción para motores de búsqueda
url: "https://tudominio.com"

plugins:
  - jekyll-seo-tag
  - jekyll-sitemap
```

```html
<!-- En layouts -->
{% seo %}
```

### Solución de problemas:
```bash
# Error de dependencias
bundle install
bundle update

# Error de permisos
bundle install --path vendor/bundle

# Sitio no actualiza
bundle exec jekyll clean
bundle exec jekyll build
```

---

## Recursos adicionales

### Documentación oficial:
- [Jekyll Docs](https://jekyllrb.com/docs/)
- [GitHub Pages](https://pages.github.com/)

### Comunidad:
- [Jekyll Talk](https://talk.jekyllrb.com/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/jekyll)

### Temas:
- [Jekyll Themes](https://jekyllthemes.io/)
- [GitHub Pages Themes](https://pages.github.com/themes/)

---

¡Felicidades! Ahora tienes todo el conocimiento necesario para crear y mantener sitios web increíbles con Jekyll. 🚀