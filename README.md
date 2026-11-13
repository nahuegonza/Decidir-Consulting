# Sitio web de Decidir Consulting

Repositorio del sitio publicado en https://decidirconsulting.netlify.app.

- `site/`: archivos del sitio (lo que se publica).
- `netlify.toml`: configuración de Netlify; publica la carpeta `site` sin comando de build.
- Cada commit en la rama `main` se publica automáticamente en Netlify.

**Conexión con Netlify (una sola vez):** en el proyecto decidirconsulting, Project configuration > Build & deploy > Continuous deployment > Link repository > GitHub > `nahuegonza/Decidir-Consulting`, rama `main`. Dejá vacío el comando de build; el directorio de publicación lo toma de `netlify.toml`.

---

# Sitio web de Decidir Consulting · Publicación en Netlify

Esta carpeta es el sitio completo, listo para publicar. No necesita instalar nada ni compilar.

## Qué hay en la carpeta

| Archivo | Para qué sirve |
|---|---|
| `index.html` | Página de inicio |
| `estrategia.html`, `cultura.html`, `liderazgo.html`, `talento.html`, `analytics.html`, `soporte-rrhh.html` | Una página por servicio |
| `diagnostico.html` | Landing de la campaña de Google Ads |
| `personas.html`, `nosotros.html`, `recursos.html`, `contacto.html` | Páginas internas |
| `privacidad.html` | Política de privacidad, cookies y términos (borrador a revisar por un abogado) |
| `404.html` | Página que se muestra si alguien entra a una dirección que no existe |
| `logo-color.png`, `logo-white.png`, `favicon.png`, `apple-touch-icon.png` | Logos e íconos |
| `netlify.toml` | Configuración de Netlify (URLs limpias y cabeceras de seguridad) |
| `robots.txt` | Permite que Google indexe el sitio |

## 1. Publicar el sitio (10 minutos)

1. Entrá a **https://app.netlify.com/signup** y creá una cuenta gratuita (podés usar tu cuenta de Google).
2. Descomprimí el archivo `decidir-netlify.zip` en tu computadora. Te queda una carpeta llamada `decidir-netlify`.
3. Entrá a **https://app.netlify.com/drop**.
4. **Arrastrá la carpeta `decidir-netlify` completa** al recuadro que dice "Drag and drop your site output folder here".
5. Esperá unos segundos. Netlify te da una dirección del tipo `https://nombre-al-azar.netlify.app`. El sitio ya está online.
6. Para cambiar ese nombre: **Site configuration > General > Site details > Change site name** y escribí, por ejemplo, `decidir-consulting`. La dirección queda `https://decidir-consulting.netlify.app`.

> Importante: arrastrá la carpeta, no el .zip, y que `index.html` quede en la raíz de lo que arrastrás (no dentro de otra subcarpeta).

## 2. Activar los formularios (5 minutos)

El sitio tiene 4 formularios conectados a **Netlify Forms**: contacto (inicio), contacto (página Contacto), diagnóstico y CV.

1. En tu sitio de Netlify andá a **Forms** (menú de la izquierda).
2. Hacé clic en **Enable form detection** (Habilitar detección de formularios).
3. **Volvé a publicar el sitio**: en **Deploys**, arrastrá otra vez la carpeta `decidir-netlify` al recuadro "Drag and drop" de esa pantalla. La detección solo funciona a partir de una nueva publicación.
4. Volvé a **Forms**: tienen que aparecer los formularios `contacto-inicio`, `contacto`, `diagnostico` y `cv`.
5. Hacé una prueba: completá el formulario de `diagnostico.html` en el sitio publicado y fijate que el envío aparezca en **Forms > diagnostico**.

### Recibir los envíos por email

1. Andá a **Site configuration > Notifications > Emails and webhooks > Form submission notifications**.
2. Hacé clic en **Add notification > Email notification**.
3. Poné el email donde querés recibir los contactos (por ejemplo `info@decidirconsulting.com.ar`) y elegí el formulario (o "Any form").
4. Repetí si querés notificaciones distintas por formulario (por ejemplo, los CV a otra casilla).

Límites a tener en cuenta: cada envío puede pesar hasta 8 MB (por eso el formulario de CV pide archivos de hasta 5 MB). Los formularios tienen un campo oculto anti-spam.

## 3. Conectar el dominio decidirconsulting.com.ar (opcional)

Hacelo solo cuando Decidir esté de acuerdo en reemplazar su sitio actual.

1. En Netlify: **Domain management > Add a domain** y escribí `decidirconsulting.com.ar`.
2. Netlify te muestra los registros DNS a configurar. Normalmente son:
   - Un registro **A** para `decidirconsulting.com.ar` apuntando a la IP que indica Netlify.
   - Un registro **CNAME** para `www` apuntando a `decidir-consulting.netlify.app` (o el nombre que hayas elegido).
3. Cargá esos registros en el proveedor donde está administrado el DNS del dominio (el hosting actual, Cloudflare o el que figure en NIC Argentina).
4. **No borres ni cambies los registros MX** (son los del email `info@decidirconsulting.com.ar`). Si los tocás, el correo deja de funcionar.
5. Esperá la propagación (de minutos a 24 horas). Netlify activa el certificado HTTPS automáticamente.

## 4. Google Analytics y Google Ads

**Google Analytics ya está incluido** en todas las páginas (ID `G-29BJT31T8B`), junto con estos eventos:

| Evento | Cuándo se registra |
|---|---|
| `generate_lead` | Cuando un formulario se envía con éxito (contacto, diagnóstico o CV) |
| `contacto_whatsapp` | Cuando alguien toca un botón de WhatsApp |
| `clic_linkedin` | Cuando alguien abre LinkedIn (perfil de Adriana, búsquedas o página de la empresa) |

> Si antes cargaste el código de Analytics con **Snippet injection** en Netlify, **borralo** (Site configuration > Build & deploy > Post processing > Snippet injection). Si queda en los dos lugares, cada visita se cuenta dos veces.

1. Publicá el sitio y entrá a Google Analytics > **Informes > Tiempo real** para ver tu visita.
2. En **Administrar > Eventos**, marcá `generate_lead` y `contacto_whatsapp` como **eventos clave**.
3. En Google Ads, vinculá la cuenta de Analytics (**Herramientas > Cuentas vinculadas > Google Analytics**) e importá esos eventos clave como conversiones.
4. Usá como URL final de los anuncios `https://TU-DOMINIO/diagnostico`. Las páginas de servicio sirven como vínculos a sitios.

## Fotos de las páginas de servicios

Las páginas de servicios muestran una foto en la carpeta `img/` (estrategia, cultura, liderazgo y soporte-rrhh: fotos propias). Talento y Analytics todavía cargan una foto provisoria de Unsplash/Pexels hasta reemplazarla por `img/talento.jpg` e `img/analytics.jpg`. Para cambiar una foto, reemplazá el archivo en `img/` con el mismo nombre (horizontal, unos 1400 px de ancho, JPG de menos de 300 KB).

La página Recursos quedó oculta: no aparece en el menú, el pie ni el inicio, y tiene `noindex` para que Google no la muestre. El archivo `recursos.html` sigue en la carpeta para reactivarla más adelante.


## Cambios del 13/11/2026 (checklist de publicación)

- **Legal:** aviso legal con titular, CUIT y domicilio; política de privacidad sin textos provisorios; enlace "Aviso legal" en el pie de todas las páginas.
- **Cookies:** aviso con "Aceptar" y "Rechazar". Google Analytics usa el modo de consentimiento: solo guarda cookies si la persona acepta. El enlace "Cookies" del pie vuelve a abrir el aviso.
- **Google:** títulos y descripciones nuevos, etiquetas para compartir en redes (imagen og-image.jpg), datos estructurados de la empresa en la portada, sitemap.xml y robots.txt con el sitemap.
- **Velocidad:** las tipografías se sirven desde la carpeta `fonts/` (ya no desde Google Fonts) y las fotos tienen versión WebP para celular y computadora.
- **Fotos:** Talento y People analytics usan ahora fotos propias de la carpeta `img/`.
- **Reseñas:** la sección de reseñas de la portada está oculta hasta cargar reseñas reales. Para mostrarla, en `index.html` borrá la palabra `hidden` de `<section class="section" id="resenas" ... hidden>` y reemplazá los textos entre corchetes.

**Dominio.** El sitemap, las URL canónicas, los datos estructurados y la imagen para redes usan `https://decidirconsulting.netlify.app`. Cuando conectes decidirconsulting.com.ar, reemplazá esa dirección por `https://decidirconsulting.com.ar` en todos los `.html`, en `sitemap.xml` y en `robots.txt`, y volvé a enviar el sitemap en Search Console.

**Después de publicar:** enviá el sitemap en Google Search Console, medí la velocidad con PageSpeed Insights y probá la vista previa del enlace en WhatsApp.

## 5. Antes de difundir el sitio: lista de pendientes

- [ ] Copiar 3 reseñas reales de Google en la sección **Reseñas** de `index.html` (texto, nombre y fecha) y reemplazar el link "Ver todas las reseñas en Google" por el de la ficha de Google Business.
- [ ] Completar `[razón social y CUIT]` y `[fecha]` en `privacidad.html`.
- [ ] Exportar el logo en alta resolución desde Canva y reemplazar `logo-color.png` y `logo-white.png` (mismo nombre de archivo, fondo transparente).
- [ ] Hacer revisar `privacidad.html` por un abogado e inscribir la base de datos en la AAIP (Ley 25.326).
- [ ] Confirmar con Decidir los textos de servicios, plazos y el "diagnóstico sin costo".
- [ ] Probar los 4 formularios y el botón de WhatsApp desde un celular.
- [ ] Los artículos de **Recursos** figuran como "Próximamente": publicarlos o quitarlos.

## 6. Cómo actualizar el sitio después

1. Editá los archivos `.html` en tu computadora (con cualquier editor de texto, por ejemplo Visual Studio Code).
2. En Netlify, andá a **Deploys** y arrastrá de nuevo la carpeta completa.
3. Si algo sale mal, en **Deploys** podés elegir una publicación anterior y hacer clic en **Publish deploy** para volver atrás.

Alternativa más profesional: subir la carpeta a un repositorio de GitHub y conectarlo en Netlify con **Add new site > Import an existing project**. Así cada cambio que subas a GitHub se publica solo.
