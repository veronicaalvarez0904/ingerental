# Ingerental SAS — Sitio web

Sitio corporativo de **Ingerental SAS** (obras civiles, movimiento de tierras, vías, concreto, urbanismos y alquiler de maquinaria).
Es una página estática (HTML, CSS y JavaScript sin dependencias) publicada con **GitHub Pages** en **https://ingerental.com**.

## Estructura

```
index.html              Página completa (estilos, contenido y scripts)
assets/img/logo.png     Logo para fondos claros (encabezado)
assets/img/logo-blanco.png  Logo para fondos oscuros (pie de página)
assets/img/favicon.png  Ícono de la pestaña
assets/img/fotos/       Carpeta para las fotografías reales
CNAME                   Dominio personalizado (ingerental.com)
robots.txt, sitemap.xml SEO
```

## Editar contenido y datos

Todo lo editable está en el bloque `CONFIG` al inicio del `<script>` de `index.html`:

| Campo | Qué es |
|---|---|
| `empresa.nit`, `direccion`, `ciudad`, `telefono`, `correo`, `horario` | Datos de contacto. Vacío = se muestra "Pendiente de configurar". |
| `empresa.whatsapp` | Número de WhatsApp con indicativo, solo dígitos. Recibe las solicitudes del formulario. |
| `empresa.redes` | URLs de Facebook, Instagram y LinkedIn. |
| `servicios` | Textos, listas y foto de cada servicio. |
| `proyectos` | Obras ejecutadas. Quite `demo:true` cuando sean proyectos reales. |
| `maquinaria` | Inventario de equipos (nombre, tipo, marca/modelo, capacidad, uso, disponibilidad, foto). |

## Fotografías y videos

Las fotos optimizadas están en `assets/img/fotos/` (JPG de máx. 1280–1600 px) y los videos en `assets/video/` (MP4 H.264 sin sonido, 10–14 s, ~3 MB, con su imagen de portada `.jpg`).

| Ubicación en la página | Archivo |
|---|---|
| Portada (video vertical) | `assets/video/hero-excavadora.mp4` |
| Fondo de "¿Tienes un proyecto en marcha?" (video de dron) | `assets/video/dron-obra.mp4` |
| Nosotros | `nosotros-equipo-campo.jpg` |
| Servicios | `movimiento-tierras.jpg`, `construccion-vias.jpg`, `drenaje-tierra-armada.jpg`, `urbanismo-cimentacion.jpg`, `alquiler-cat-312c.jpg` |
| Proyectos | `proyecto-*.jpg` |
| Maquinaria y flota | `flota-patio.jpg`, `equipo-*.jpg` |
| Vista previa al compartir (Open Graph) | `og-ingerental.jpg` |

Para cambiar una imagen: súbala a `assets/img/fotos/` y ponga la ruta en `CONFIG` (`fotos`, `servicios[].foto`, `proyectos[].foto` o `maquinaria[].foto`).
Para un video: campo `video` en `CONFIG.fotos` (con `src` como portada). Si el navegador no puede reproducirlo, o el visitante tiene activado "reducir movimiento", se muestra la portada.

Para preparar un video nuevo (requiere ffmpeg):
```bash
ffmpeg -ss 5 -t 12 -i original.MOV -an -vf "scale=1280:-2,fps=30,format=yuv420p" -c:v libx264 -crf 28 -movflags +faststart assets/video/nuevo.mp4
```

Use solo fotos propias y evite placas de vehículos o rostros sin autorización.

## Formulario de cotización (WhatsApp)

El formulario no envía correos ni usa servidores. Al presionar **Enviar por WhatsApp**:
1. Valida los campos obligatorios y el formato del correo.
2. Abre WhatsApp (app o WhatsApp Web) con la solicitud ya redactada, dirigida al número de `empresa.whatsapp`.
3. El visitante solo presiona *Enviar* en WhatsApp.

Además hay un botón "Escríbenos por WhatsApp" en la portada y un botón flotante en todas las secciones.
Para cambiar el número, edite `empresa.whatsapp` (solo dígitos con indicativo, ej. `573006106404`).

## Publicación (GitHub Pages + GoDaddy)

**GitHub:** Settings → Pages → Source: *Deploy from a branch*, rama `main`, carpeta `/ (root)`. Custom domain: `ingerental.com`. Activar *Enforce HTTPS* cuando esté disponible.

**GoDaddy → ingerental.com → DNS**, registros:

| Tipo | Nombre | Valor |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | veronicaalvarez0904.github.io |

Elimine el registro A de "Parked"/WebsiteBuilder y cualquier reenvío (forwarding) del dominio. La propagación toma de minutos a unas horas; el certificado HTTPS lo emite GitHub automáticamente.

## Probar en local

Abra `index.html` en el navegador, o sirva la carpeta:

```bash
python3 -m http.server 8080
# http://localhost:8080
```

## Estado

**Operativo:** fotos y videos reales, envío de solicitudes por WhatsApp (formulario, botón en portada y botón flotante), navegación y menú móvil, detalle de servicios, filtros de proyectos, fichas de maquinaria, validaciones del formulario, SEO básico (título, descripción, Open Graph, sitemap).

**Por completar:** verificar nombres, ubicaciones y descripciones de proyectos; capacidades y disponibilidad de cada equipo.
