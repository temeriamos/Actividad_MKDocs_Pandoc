# Instalación de Librerías para MkDocs con Exportación a PDF

Este documento detalla los pasos necesarios para instalar las librerías requeridas y solucionar errores comunes al compilar (`build`) un sitio de documentación con MkDocs y exportación a PDF.

## Paso 1: Crear y Activar un Entorno Virtual (Opcional pero Recomendado)

Para mantener un entorno limpio y evitar conflictos con otras librerías, se recomienda el uso de un entorno virtual (`venv`). Para crearlo y activarlo, sigue estos pasos:

### En macOS/Linux:
```bash
python3 -m venv venv
source venv/bin/activate
```

### En Windows (PowerShell):
```powershell
python -m venv venv
venv\Scripts\activate
```

---

## Paso 2: Instalar MkDocs y Plugins Necesarios

Instala MkDocs y los plugins necesarios ejecutando:
```bash
pip install mkdocs mkdocs-material mkdocs-with-pdf qrcode[pil]
```

Si estás usando `mkdocs-pdf-export-plugin`, instala también:
```bash
pip install mkdocs-pdf-export-plugin
```

---

## Paso 3: Verificar la Instalación de Dependencias

Para asegurarte de que todas las librerías necesarias están instaladas, ejecuta:
```bash
pip list | grep mkdocs
```
Esto debería mostrar algo similar a:
```
mkdocs                     x.x.x
mkdocs-material            x.x.x
mkdocs-with-pdf            x.x.x
mkdocs-pdf-export-plugin   x.x.x
```
Si alguna falta, instálala manualmente con `pip install`.

---

## Paso 4: Configurar `mkdocs.yml`

Asegúrate de que tu archivo `mkdocs.yml` esté correctamente configurado, con las siguientes opciones:
```yaml
site_name: My Docs
site_image: 'images/logo.png'
site_favicon: 'images/favicon.ico'
docs_dir: docs_src
site_dir: docs
site_description: A simple documentation site
site_author: Carlos Miguel
site_url: https://temeriamos.github.io/Actividad_MKDocs_Pandoc.git

nav:
  - Home: index.md
  - About: about.md
  - Contact: contact.md
  - PDF: pdf.md

theme: material

plugins:
  - search
  - pdf-export
  - with-pdf:
      author: 'Temeriamos'
      copyright: '2022'
      cover: true
      back_cover: true
      cover_title: 'My Docs'
      cover_subtitle: 'Manual de usuario'
      toc_title: 'Contenido'
      toc_levels: 2
      ordered_chapters_level: 2
      output_path: pdf/documentacionCompleta.pdf
```

Si usas `mkdocs-pdf-export-plugin`, reemplaza `with-pdf` por:
```yaml
  - pdf-export
```

---

## Paso 5: Solucionar Errores Comunes

### Error 1: `cannot load library 'libpango-1.0-0'`
Este error ocurre porque falta la librería `pango`, que es requerida por `WeasyPrint`.

🔹 **Solución en macOS/Linux:**
```bash
brew install pango cairo gobject-introspection
pip install --force-reinstall weasyprint
```

🔹 **Solución en Windows:**
1. Descarga e instala `GTK+` desde: [https://gtk.org/](https://gtk.org/)
2. Luego, reinstala WeasyPrint:
   ```bash
   pip install --force-reinstall weasyprint
   ```

### Error 2: `PluginNotFoundError: No module named 'mkdocs-with-pdf'`
🔹 **Solución:**
Reinstala el plugin con:
```bash
pip install --upgrade mkdocs-with-pdf
```

### Error 3: `The theme 'readthedocs' is not found`
🔹 **Solución:**
Si `readthedocs` no está disponible, instala el tema `mkdocs-material`:
```bash
pip install mkdocs-material
```
O cambia en `mkdocs.yml`:
```yaml
theme: material
```

### Error 4: `No module named 'qrcode'`
🔹 **Solución:**
Si falta la librería de códigos QR, instálala con:
```bash
pip install qrcode[pil]
```

---

## Paso 6: Construir y Servir el Sitio

Una vez instaladas todas las dependencias, genera el sitio con:
```bash
mkdocs build
```

Si deseas visualizar el sitio en local antes de desplegarlo:
```bash
mkdocs serve
```
Esto iniciará un servidor en `http://127.0.0.1:8000/` donde podrás ver la documentación.

---

## Conclusión
Siguiendo estos pasos, deberías poder generar documentación con MkDocs y exportarla a PDF sin errores. Si sigues teniendo problemas, verifica los mensajes de error y asegúrate de que todas las librerías están correctamente instaladas.

¡Éxito con tu documentación! 🚀

