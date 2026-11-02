# Plantilla NoExpertise · Escuela infantil

Web alegre para escuelas infantiles y ludotecas, con aulas por edades, horario, equipo y matrícula.

- Sectores: escuela-infantil, guarderia, ludoteca, campamentos, extraescolares. Estilo: alegre. Plan mínimo: presencia.
- Secciones: hero, aulas, horario, equipo, proyecto, matricula, galeria, opiniones, preguntas, contacto (más el diseño `texto` para apartados nuevos).
- A ancho completo: todas las secciones son bandas de borde a borde (amarillo, azul, verde, crema y noche), con portada partida a sangre, aulas en bloques de color sin márgenes, fotos a sangre 50/50, mosaico de galería sin márgenes y festones entre bandas.
- Campos propios: `aulas[]` (nombre, edades, texto, precio, imagen), `horario.horario[]` + `horario.jornada[]` (un día en la escuela), `proyecto.declaracion` y `firma` (cita grande), `matricula.items` (pasos) con formulario de visita y desplegable de aulas, `opiniones.testimonios[].detalle`, `hero.destacado` (pegatina).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`ChildCare`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos de la demo en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.aulas.aulas` con `detalle` tiene su página en `/aulas/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
