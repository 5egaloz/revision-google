# Vitrina de automotora

Página de una automotora: el patio con los autos disponibles, la ficha de cada
uno con el mensaje de WhatsApp ya escrito, y un panel donde el dueño publica,
sube la foto y marca vendido.

En vivo: <https://5egaloz.github.io/revision-google/automotora/>

Un solo `index.html`, sin build ni dependencias. Se abre con doble clic y anda.

## De dónde saca los autos

Por orden de prioridad:

1. **`stock.json`** publicado junto a esta página, si existe. Es el stock que ve
   todo el mundo, y es el archivo que escribe el flujo de WhatsApp.
2. **El borrador de este navegador** (`localStorage`), si el dueño publicó algo
   desde el panel. Solo lo ve él, en ese equipo. El panel avisa cuando está en
   este caso; el botón «Volver al stock de ejemplo» lo borra.
3. **Los siete vehículos de ejemplo** que van dentro del HTML, para que la demo
   funcione aunque no haya nada más.

El formato de `stock.json` está en `stock.ejemplo.json`. Todo lo que entra se
normaliza y se escapa antes de mostrarse: un modelo escrito con etiquetas HTML
sale como texto, no como código.

## Lo que falta para que sea el sitio real

### 1. El panel tiene que dejar de vivir acá

Hoy la clave (`CLAVE_DEMO`) está escrita en el código, a la vista de cualquiera
que abra «ver código fuente». **Va así a propósito y no es seguridad**: es una
demostración con datos inventados, y un hash acá parecería seguro sin serlo.

En el sitio real el panel va en otra URL, detrás de autenticación de servidor
(Caddy o n8n), y su archivo no se sube al repo público. Mismo criterio que el
`mostrador.html` de Llega y Retira.

### 2. Los autos entran por WhatsApp, no a mano

La API de WhatsApp Business **no da acceso a los estados/historias**: no hay
endpoint que los lea, y leerlos con una sesión automatizada de WhatsApp Web
rompe los términos de uso y arriesga el número del cliente.

El camino que sí funciona, y que es el mismo patrón que ya corre en Llega y
Retira y en Control de Leña:

```
el dueño reenvía su publicación al bot  →  n8n recibe foto + texto
   →  Gemini visión saca marca, modelo, año, km y precio
   →  se arma el registro y se escribe stock.json
   →  la vitrina lo muestra sin tocar el HTML
```

El dueño no aprende nada nuevo: sigue publicando su estado como siempre y
además lo reenvía al bot. Un paso, no un sistema.

### 3. Dominio propio

Cuando haya dominio:

- Archivo `CNAME` en la raíz del repo con el dominio, y los registros DNS
  apuntando a GitHub Pages.
- Cambiar en `index.html` la etiqueta `<link rel="canonical">` y las tres
  `og:*` que llevan la URL.
- Actualizar `sitemap.xml` y `robots.txt` de la raíz.

Mientras tanto todo eso apunta a la URL de GitHub Pages, que es la que está
viva.
