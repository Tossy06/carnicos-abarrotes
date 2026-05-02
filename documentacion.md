# Documentación — Taller práctico de GitHub

Registro completo del flujo de trabajo utilizado para crear, versionar y publicar el sitio web **Cárnicos & Abarrotes** usando Git, GitHub CLI y GitHub Pages.

---

## Herramientas utilizadas

| Herramienta | Versión | Uso |
|---|---|---|
| **Git** | 2.x | Control de versiones local |
| **GitHub CLI (`gh`)** | 2.x | Gestión de repositorio, PRs y Pages desde terminal |
| **VS Code** | — | Editor de código |
| **Bootstrap** | 5.3.0 | Framework CSS para diseño responsivo |
| **Bootstrap Icons** | 1.11.0 | Biblioteca de iconos SVG |
| **Google Fonts — Inter** | — | Tipografía principal del sitio |

---

## 1. Configuración de identidad local

Antes de hacer cualquier commit, Git necesita saber quién eres. Esta configuración se guarda globalmente en el equipo.

```bash
git config user.name "Tossy06"
git config user.email "tu@email.com"
```

> Verificar la configuración guardada:
> ```bash
> git config --list
> ```

---

## 2. Inicializar repositorio local

Se crea la carpeta del proyecto y se inicializa un repositorio Git vacío dentro de ella.

```bash
mkdir carnicos-abarrotes
cd carnicos-abarrotes
git init
```

`git init` crea la carpeta oculta `.git/` que almacena todo el historial de versiones del proyecto.

---

## 3. Crear repositorio en GitHub

Con GitHub CLI se crea el repositorio remoto directamente desde la terminal, sin necesidad de entrar al navegador.

```bash
gh repo create carnicos-abarrotes --public
```

| Opción | Descripción |
|---|---|
| `carnicos-abarrotes` | Nombre del repositorio en GitHub |
| `--public` | El repositorio será visible para todos (necesario para GitHub Pages gratuito) |

---

## 4. Conectar repositorio local con GitHub

Se vincula el repositorio local con el remoto recién creado y se establece `main` como rama principal.

```bash
git remote add origin https://github.com/Tossy06/carnicos-abarrotes.git
git branch -M main
```

| Comando | Qué hace |
|---|---|
| `git remote add origin <url>` | Registra el repositorio remoto con el alias `origin` |
| `git branch -M main` | Renombra la rama actual a `main` |

---

## 5. Estructura inicial del sitio

Se crean los archivos y carpetas del proyecto antes del primer commit.

```bash
touch index.html productos.html contacto.html
mkdir css img
touch css/style.css
```

Estructura resultante:

```
carnicos-abarrotes/
├── index.html
├── productos.html
├── contacto.html
├── css/
│   └── style.css
└── img/
```

---

## 6. Primer commit y push

Se agregan todos los archivos al área de staging, se crea el primer commit y se sube al repositorio remoto.

```bash
git add .
git commit -m "Estructura inicial del sitio"
git push -u origin main
```

| Comando | Qué hace |
|---|---|
| `git add .` | Agrega todos los archivos modificados al área de staging |
| `git commit -m "..."` | Guarda una instantánea del proyecto con un mensaje descriptivo |
| `git push -u origin main` | Sube los cambios a GitHub; `-u` guarda `origin main` como destino por defecto |

---

## 7. Rama — Catálogo de productos

Se trabaja la sección del catálogo en una rama separada para no afectar `main` mientras se desarrolla.

```bash
# Crear y moverse a la nueva rama
git checkout -b feature/catalogo

# Editar productos.html con la sección de cárnicos y abarrotes...

# Registrar cambios
git add .
git commit -m "Agrega sección catálogo de productos"

# Subir la rama a GitHub
git push origin feature/catalogo

# Crear Pull Request y fusionarlo a main
gh pr create --title "Catálogo de productos" \
  --body "Se agrega sección de cárnicos y abarrotes con Bootstrap e iconos" \
  --base main
gh pr merge feature/catalogo --merge
```

**Flujo de trabajo con ramas:**

```
main ─────────────────────���────────────► main
      └── feature/catalogo ──► PR #1 ──┘
```

---

## 8. Rama — Página de contacto

Mismo flujo: rama nueva → desarrollo → commit → PR → merge.

```bash
git checkout main
git pull origin main                    # Sincronizar main con los últimos cambios
git checkout -b feature/contacto

# Editar contacto.html...

git add .
git commit -m "Agrega página de contacto"
git push origin feature/contacto

gh pr create --title "Página de contacto" \
  --body "Se agrega formulario de contacto e información de la empresa" \
  --base main
gh pr merge feature/contacto --merge
```

> Siempre hacer `git pull origin main` antes de crear una rama nueva para partir del código más actualizado.

---

## 9. Rama — Galería

```bash
git checkout main
git pull origin main
git checkout -b feature/galeria

# Editar index.html con la galería de imagen de marca...

git add .
git commit -m "Agrega galería e imagen de marca en index"
git push origin feature/galeria

gh pr create --title "Galería e imagen de marca" \
  --body "Se agrega galería de imagen corporativa y página de inicio completa" \
  --base main
gh pr merge feature/galeria --merge
```

---

## 10. Resumen de Pull Requests

| PR | Rama | Descripción |
|---|---|---|
| #1 | `feature/catalogo` | Catálogo de productos con cárnicos y abarrotes |
| #2 | `feature/contacto` | Formulario de contacto e información de la empresa |
| #3 | `feature/galeria` | Galería corporativa y página de inicio completa |

---

## 11. Actualizar main y publicar con GitHub Pages

Una vez fusionadas todas las ramas, se actualiza `main` localmente y se activa GitHub Pages.

```bash
# Actualizar main local
git checkout main
git pull origin main

# Activar GitHub Pages desde la API de GitHub
gh api repos/Tossy06/carnicos-abarrotes/pages \
  --method POST \
  --input - <<'EOF'
{"source":{"branch":"main","path":"/"}}
EOF
```

| Campo | Valor | Descripción |
|---|---|---|
| `branch` | `main` | Rama desde la cual se publica el sitio |
| `path` | `/` | Carpeta raíz del repositorio |

GitHub Pages tarda entre 1 y 3 minutos en desplegar el sitio por primera vez.

> Verificar el estado de la publicación:
> ```bash
> gh api repos/Tossy06/carnicos-abarrotes/pages
> ```

---

## 12. Convenciones de commits

Los mensajes de commit del proyecto siguen el formato imperativo en español:

| Tipo | Ejemplo |
|---|---|
| Nueva funcionalidad | `Agrega página de contacto` |
| Corrección | `Corrige alineación del hero en mobile` |
| Estilos | `Actualiza paleta de colores y tipografía` |
| Documentación | `Agrega README y documentación del proyecto` |

---

## Resultado final

| | |
|---|---|
| **Repositorio** | https://github.com/Tossy06/carnicos-abarrotes |
| **Sitio publicado** | https://tossy06.github.io/carnicos-abarrotes/ |
| **Ramas creadas** | 3 (`feature/catalogo`, `feature/contacto`, `feature/galeria`) |
| **Pull Requests** | 3 (todos fusionados a `main`) |
| **Páginas del sitio** | 3 (`index.html`, `productos.html`, `contacto.html`) |
