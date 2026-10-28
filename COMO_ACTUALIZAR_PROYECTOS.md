# Cómo publicar nuevas fotos de proyectos

Esta versión mantiene la carga de imágenes dentro del administrador de archivos de Hostinger para evitar que cualquier visitante pueda subir archivos al servidor.

1. Prepare la fotografía en formato JPG o WebP, preferiblemente horizontal, con un ancho de 1600 píxeles y un peso menor a 500 KB.
2. Use un nombre corto, sin espacios ni tildes, por ejemplo: `avance-auca-julio-2026.jpg`.
3. En Hostinger, abra **Administrador de archivos > public_html > assets** y cargue la fotografía.
4. En `index.html`, duplique una tarjeta dentro del bloque `project-gallery`.
5. Cambie el nombre de la imagen, el proyecto, la ubicación, la descripción y las etiquetas.
6. Use una de estas categorías en `data-category`: `construccion`, `mantenimiento` o `facilidades`.

No se recomienda colocar un formulario público de carga sin contraseña, validación y almacenamiento seguro. Si BARVILL necesita publicar semanalmente, el siguiente paso adecuado es crear un panel privado con usuario y contraseña.

## Cómo publicar una noticia / avance de obra

La sección **Noticias y avances de obra** (`id="noticias"`) es para actualizaciones cortas y frecuentes — a diferencia de "Proyectos", que es el portafolio curado.

1. Prepare la fotografía igual que en el paso 1 de arriba y súbala a **Administrador de archivos > public_html > assets**.
2. En `index.html`, dentro de `<div class="news-feed">`, duplique un bloque `<article class="news-card">` completo (incluyendo su etiqueta de cierre).
3. En el nuevo bloque, cambie:
   - El `src` y el `alt` de la imagen.
   - El mes y año en `<span class="news-date">`.
   - El título en `<h3>`.
   - El texto breve en `<p>`.
4. Coloque la noticia más reciente primero (arriba de las demás).
5. No es necesario borrar noticias antiguas, pero si la lista crece mucho conviene dejar solo las últimas 6-8 y archivar el resto.

Igual que con las fotos de proyectos, si BARVILL necesita publicar noticias muy seguido, conviene evaluar un panel privado en vez de editar `index.html` manualmente cada vez.

### Noticia destacada con video y varias fotos (como "Proyecto Shaya")

Para una noticia con más material (varias fotos + un video corto), use `<article class="news-card news-card-featured">` en vez de la tarjeta simple. Tome como modelo el bloque "Proyecto Shaya" ya incluido en `index.html`.

1. Videos: formato MP4, idealmente menos de 15-20 segundos y menos de 5 MB para que cargue rápido (el reproductor solo carga los metadatos hasta que el visitante presiona play, gracias a `preload="metadata"`).
2. Suba el video a `assets/` igual que las fotos (nombre corto, sin espacios ni tildes).
3. La imagen en `poster="..."` es la miniatura que se ve antes de reproducir — use una de las fotos de la misma noticia.
4. Cada foto de la galería va en un `<button data-lightbox="assets/archivo.jpg">` con su `<img>` adentro — al hacer clic se amplía igual que en "Proyectos". Puede tener 2, 3 o más fotos.
5. Si no tiene video para una noticia, use la tarjeta simple (`class="news-card"`) como las demás.

## Importante: si edita el bloque de datos estructurados (JSON-LD)

El archivo `index.html` incluye un bloque `<script type="application/ld+json">` (justo debajo de las etiquetas `<meta property="og:...">`) con los datos de la empresa para buscadores. La política de seguridad (`Content-Security-Policy` en `.htaccess`) solo permite ejecutar ese bloque exacto mediante un "hash" de su contenido.

**Si edita cualquier carácter dentro de ese bloque JSON-LD** (por ejemplo, el teléfono, la dirección o el logo), el hash debe recalcularse y actualizarse en `.htaccess`, o el buscador dejará de leer esos datos silenciosamente (sin mostrar ningún error visible en la página). Si no sabe cómo recalcular el hash, pida ayuda antes de publicar el cambio.
