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
| `empresa.politicaPrivacidad` | URL de la política de tratamiento de datos (Ley 1581 de 2012). |
| `empresa.redes` | URLs de Facebook, Instagram y LinkedIn. |
| `servicios` | Textos, listas y foto de cada servicio. |
| `proyectos` | Obras ejecutadas. Quite `demo:true` cuando sean proyectos reales. |
| `maquinaria` | Inventario de equipos (nombre, tipo, marca/modelo, capacidad, uso, disponibilidad, foto). |

## Fotografías

1. Suba las fotos a `assets/img/fotos/` (JPG o WebP, máximo ~300 KB cada una, horizontales de 1600 px para el hero).
2. En `CONFIG`, ponga la ruta en el campo correspondiente, por ejemplo:
   `fotos.hero.src: "assets/img/fotos/hero.jpg"` o `servicios[0].foto: "assets/img/fotos/movimiento-tierras.jpg"`.
3. Si un campo queda vacío, la página muestra el espacio reservado con la descripción de la foto que va ahí.

Use solo fotos propias o con licencia, y no presente obras de terceros como propias.

## Formulario de cotización (WhatsApp)

El formulario no envía correos ni usa servidores. Al presionar **Enviar por WhatsApp**:
1. Valida los campos obligatorios, el formato del correo y la autorización de datos.
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

**Operativo:** envío de solicitudes por WhatsApp (formulario, botón en portada y botón flotante), navegación y menú móvil, detalle de servicios, filtros de proyectos, fichas de maquinaria, validaciones del formulario, SEO básico (título, descripción, Open Graph, sitemap).

**Requiere configuración:** fotos reales, datos de contacto, NIT, redes, política de privacidad, proyectos reales e inventario de maquinaria.
