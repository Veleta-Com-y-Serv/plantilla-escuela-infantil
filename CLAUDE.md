# Plantilla «Escuela infantil» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **alegre**.
Todo en castellano de España, frases cortas, sin jerga. El diseño y su porqué están en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = azul, acento = amarillo, fondo = crema, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…, y calcula `--c-sobre-primario`/`--c-sobre-acento`, el texto legible encima) y Tailwind los expone como `bg-primario`, `text-acento`… Los derivados se calculan con `color-mix` en `src/styles/global.css`: `--verde` (mezcla del primario y el acento en OKLCH: azul + amarillo = verde), `--noche` (primario muy oscuro, pie y un aula), `--amarillo-claro`, `--azul-claro`, `--verde-claro` y `--linea`.
- **Tipografía y aspecto general**: `src/styles/global.css`. Sans redondeada del sistema (`ui-rounded`, Nunito o Arial Rounded si están; si no, la del sistema) a peso 900 en títulos. Bandas a todo el ancho `.banda` + `.banda-amarilla | -azul | -verde | -crema | -clara | -noche`; festón (medias lunas que cuelgan sobre la banda siguiente) `.feston` y, en el pie, `.feston-arriba`; botones píldora `.btn` (primario), `.btn-amarillo`, `.btn-claro`, `.btn-sec`; `.bola` (icono en círculo), `.pildora`, `.arcoiris`; paneles a sangre `.paneles/.panel`; fila foto/texto a sangre `.fila-sangre`. Cabecera `.cabecera--cometa` y pie `.pie--noche`. Sin fuentes externas.
- **Formas decorativas**: `src/components/ui/Forma.astro` (nube, estrella, sol, cometa, garabato; color con `currentColor`, siempre `aria-hidden`). Sello de la marca sin logo: `src/components/ui/Sello.astro` (círculo, cuadrado y triángulo).
- **Imágenes**: en `public/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las fotos de la demo se generan a partir de `fotos.json`; mientras una foto `/fotos/x.jpg` no exista, `Imagen.astro` usa su respaldo `/placeholders/x.svg`. Las fotos nuevas del cliente van en `public/fotos/`.
- **Personas**: `personas[].foto` usa la silueta `/placeholders/persona.svg` salvo que el cliente aporte su foto. No se generan caras.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = sello de tres piezas + nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie`.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`. `hero` y `contacto` son obligatorias. Todas son bandas a todo el ancho de la ventana; cada componente lleva su color.
- `hero` → `secciones/hero.astro` (partida: bloque amarillo con el texto | foto a sangre con esquina grande, pegatina redonda; festón)
- `aulas` → `secciones/aulas.astro` (crema; fila de bloques de color de borde a borde, uno por aula)
- `horario` → `secciones/horario.astro` (azul; horas grandes, servicios y «un día en la escuela»; festón)
- `equipo` → `secciones/equipo.astro` (crema; retratos en arco)
- `proyecto` → `secciones/proyecto.astro` (verde; foto a sangre 50/50, pilares y cita grande en banda amarilla)
- `matricula` → `secciones/matricula.astro` (dos paneles a sangre: azul con pasos | amarillo claro con formulario)
- `galeria` → `secciones/galeria.astro` (mosaico de borde a borde sin márgenes)
- `opiniones` → `secciones/opiniones.astro` (amarillo; bocadillos de colores; festón)
- `preguntas` → `secciones/preguntas.astro` (crema; acordeón `details/summary`)
- `contacto` → `secciones/contacto.astro` (azul; datos y formulario | plano a sangre)
- Diseño extra para apartados nuevos: `texto` (genérico; con imagen, fila 50/50 a sangre).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. **Precios siempre como cadena** (`precio: "desde 290 €/mes"`); precio vacío = no se muestra.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Si un aula necesita varios valores, usa una cadena. Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Apartado nuevo**: añade `secciones.<id-nuevo>` en `site.yaml` con `tipo:` igual al diseño que quieras (`texto`, `aulas`, `horario`, `equipo`, `proyecto`, `preguntas`…). Si ninguno sirve, crea `src/components/secciones/<id>.astro` copiando la estructura de uno existente (`seccion(Astro.props.id)`, una `<section class="banda banda-…">`, `Titular`). `src/pages/index.astro` lo recoge solo: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto (`.contenedor` o `--margen-panel`), las bandas y fotos a sangre de borde a borde y sin scroll horizontal en móvil (las bandas llevan `overflow-x: clip`; las formas van dentro). Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`, o el nombre de la persona); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml` y llevan los campos en el cuerpo. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro` y en `matricula.astro`.
10. Nunca inventes precios, cifras, opiniones ni datos que el cliente no haya dado: deja el campo vacío o la lista vacía (los componentes lo ocultan).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `hero.destacado` {titulo, texto}: pegatina redonda verde sobre la foto («Matrícula abierta · Curso 2027-2028»). `hero.items`: 3 etiquetas con `titulo` e `icono`. `hero.cta` y `hero.cta_secundario`.
- `aulas.aulas[]`: `{ nombre, edades, texto, precio, imagen }`. Los campos vacíos no se pintan; sin aulas solo queda el titular. `aulas.cta`: botón de cada aula (lleva a la matrícula y deja elegida esa aula en el desplegable).
- `horario.horario[]` {dia, horas}: las horas en grande (también salen en el pie y en el horario de Google). `horario.nota`. `horario.items[]` {titulo, texto, icono}: servicios. `horario.jornada_titulo` y `horario.jornada[]` {hora, titulo, icono}: «un día en la escuela» (sin momentos no se pinta).
- `equipo.personas[]`. Sin personas, la sección no se pinta.
- `proyecto.texto` (párrafos separados por una línea en blanco), `proyecto.imagen`, `proyecto.items[]` (pilares con `icono`), `proyecto.declaracion` (cita enorme en banda amarilla; vacía = sin banda) y `proyecto.firma`.
- `matricula.items[]` {titulo, texto}: pasos numerados. `matricula.nota`, `matricula.boton`. Formulario: nombre, email, teléfono, aula (desplegable con los `nombre` de `aulas` de todas las secciones activas), fecha de nacimiento, cuándo empezar y mensaje.
- `galeria.galeria[]`: rutas de fotos (mosaico; mejor 6 o múltiplos de 6). Sin fotos no se pinta.
- `opiniones.testimonios[]` {texto, autor, detalle}. Sin opiniones no se pinta.
- `preguntas.preguntas[]` en acordeón; `preguntas.cta` opcional.
- `contacto.imagen`: plano a sangre que enlaza a mapas (sin plano, el formulario pasa a la derecha). `contacto.boton`.
- Iconos disponibles (`icono:`): los de `src/components/ui/Icono.astro` (p. ej. `nino`, `cubiertos`, `hoja`, `sol`, `luna`, `globo`, `pelota`, `mensaje`, `taza`, `musica`, `casa`, `estrella`, `corazon`, `pincel`, `nube`, `cometa`, `libro`, `reloj`, `check`).
