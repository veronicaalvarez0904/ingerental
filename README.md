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
| `empresa.whatsapp` | Número con indicativo, solo dígitos (ej. `573001234567`). Activa el botón flotante y el envío por WhatsApp. |
| `empresa.politicaPrivacidad` | URL de la política de tratamiento de datos (Ley 1581 de 2012). |
| `empresa.redes` | URLs de Facebook, Instagram y LinkedIn. |
| `formulario.endpoint` | URL que recibe las solicitudes (ver abajo). |
| `servicios` | Textos, listas y foto de cada servicio. |
| `proyectos` | Obras ejecutadas. Quite `demo:true` cuando sean proyectos reales. |
| `maquinaria` | Inventario de equipos (nombre, tipo, marca/modelo, capacidad, uso, disponibilidad, foto). |

## Fotografías

1. Suba las fotos a `assets/img/fotos/` (JPG o WebP, máximo ~300 KB cada una, horizontales de 1600 px para el hero).
2. En `CONFIG`, ponga la ruta en el campo correspondiente, por ejemplo:
   `fotos.hero.src: "assets/img/fotos/hero.jpg"` o `servicios[0].foto: "assets/img/fotos/movimiento-tierras.jpg"`.
3. Si un campo queda vacío, la página muestra el espacio reservado con la descripción de la foto que va ahí.

Use solo fotos propias o con licencia, y no presente obras de terceros como propias.

## Formulario de cotización

Sin `formulario.endpoint`, el formulario valida los datos pero **no envía nada** y se lo dice al usuario (le ofrece copiar el resumen o enviarlo por WhatsApp si está configurado).

Para recibir solicitudes por correo, la opción más simple es [Formspree](https://formspree.io):
1. Cree un formulario en Formspree con el correo comercial.
2. Copie la URL (ej. `https://formspree.io/f/abcdwxyz`) en `formulario.endpoint`.
3. Haga un envío de prueba y confirme el correo de activación.

También sirve cualquier servicio o API que acepte `POST` con JSON (Getform, Make, n8n, backend propio).

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

**Operativo:** navegación y menú móvil, detalle de servicios, filtros de proyectos, fichas de maquinaria, validaciones del formulario, SEO básico (título, descripción, Open Graph, sitemap).

**Requiere configuración:** fotos reales, datos de contacto, NIT, WhatsApp, redes, política de privacidad, endpoint del formulario, proyectos reales e inventario de maquinaria.
