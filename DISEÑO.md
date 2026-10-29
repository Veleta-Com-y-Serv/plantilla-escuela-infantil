# Escuela infantil: brief de diseño

Plantilla `escuela-infantil` creada el 29/10/2026 a partir de `academia-formacion` con `php artisan plantillas:nueva`
y rediseñada entera (tanda «ancho completo», fila 20 del brief). Este fichero se queda en el repo: es lo que lee
quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: escuelas infantiles (0-3 años), guarderías, ludotecas, campamentos y extraescolares. Quien entra
  es una familia que busca plaza: quiere ver las aulas por edades, el horario, quién cuida a su peque y cómo pedir
  una visita.
- **Qué tiene que conseguir la web**: que la familia pida una visita o reserve plaza (botón de cabecera, formulario
  de matrícula, teléfono y WhatsApp).
- **Tono y estilo** (`alegre`): alegre, cálido, ordenado. Sí: juguetes de madera, bloques de construcción, cuentos
  ilustrados, la referencia de ritmo de bandas de losmartesnohayluna.com. No: caja centrada con tarjetas blancas,
  colores pastel desvaídos, dibujos infantiles recargados.
- **Concepto**: «bloques de colores». Tres colores primarios en bloques grandes de borde a borde, como piezas de
  construcción: amarillo (acento), azul (primario) y **verde, que sale de mezclar los dos** (`color-mix` en OKLCH),
  más crema de fondo y un azul noche derivado para el pie. Esquinas muy redondeadas (arcos, píldoras, esquinas de
  12 rem en las fotos a sangre), **festones** de medias lunas que cuelgan de una banda sobre la siguiente y formas
  de juguete sueltas (nube, estrella, sol, cometa, arcoíris de tres arcos, garabato).
- **Paleta de ejemplo**: primario `#2152d9`, acento `#ffd23f`, fondo `#fffaf0`, texto `#1b2340`. El diseño aguanta
  otros cuatro: el verde, el noche y los claros se derivan; el texto sobre primario y acento se calcula en
  `Base.astro`. Si el primario y el acento están en lados opuestos del círculo cromático, la mezcla puede tirar
  hacia otro tono: sigue siendo un color intermedio de los dos.
- **Tipografía**: sans redondeada del sistema (`ui-rounded` en Apple, Nunito o Arial Rounded si están instaladas;
  si no, la del sistema) a peso 900 y con interletrado negativo en títulos enormes (hasta 6,75 rem en la portada);
  antetítulos en mayúsculas espaciadas con una pastilla de tres colores delante. Sin fuentes externas.
- **Ritmo de bandas**: portada amarilla partida → aulas (crema + bloques amarillo/azul/verde/noche) → horario azul
  → equipo crema → proyecto verde + cita amarilla → matrícula azul | amarillo claro → galería a sangre → opiniones
  amarillas → preguntas crema → contacto azul | plano → pie noche.

## Apartados

1. `hero`: partida 50/50 a sangre (88 svh en escritorio): bloque amarillo con antetítulo, título enorme, texto, dos
   botones y tres etiquetas con icono; foto hasta el borde con esquina inferior izquierda de 12 rem; pegatina
   redonda verde (`destacado`) sobre la unión; nube, estrella y arcoíris. En móvil, texto arriba y foto a sangre
   debajo con la esquina arriba.
2. `aulas` (`aulas[]`: nombre, edades, texto, precio, imagen): fila de bloques de color sin márgenes (4 columnas en
   escritorio, 2 en tableta, 1 en móvil); foto en arco con pastilla de edades; botón que deja elegida el aula en la
   matrícula.
3. `horario` (`horario[]` dia/horas, `nota`, `items[]` servicios con icono, `jornada[]` hora/titulo/icono):
   banda azul; horas en amarillo enorme; servicios en 2 columnas con línea de puntos; «un día en la escuela» en
   fila de 6 bolas unidas por una línea discontinua.
4. `equipo` (`personas[]`): retratos en arco sobre fondos de color, 4 columnas (2 en móvil).
5. `proyecto` (texto, imagen, `items[]` pilares, `declaracion`, `firma`): banda verde con foto a sangre a la
   izquierda; pilares en 4 columnas; cita enorme en banda amarilla con sol y cometa.
6. `matricula` (`items[]` pasos, `nota`, `boton`): dos paneles a sangre, azul con pasos numerados unidos por una
   línea de puntos y teléfono/WhatsApp, y amarillo claro con el formulario (mailto).
7. `galeria` (`galeria[]`): mosaico de borde a borde sin márgenes, patrón de 6 (grande, anchas y normales) con
   esquinas «de pompa».
8. `opiniones` (`testimonios[]` texto/autor/detalle): bocadillos de cómic de colores en banda amarilla.
9. `preguntas`: acordeón de burbujas gorditas que se tiñen de amarillo al abrirse.
10. `contacto`: banda azul partida, datos con bola amarilla y formulario | plano a sangre.
- `texto` (diseño genérico): banda amarillo claro; con imagen, fila 50/50 a sangre con la foto a la derecha.

## Fotos

`fotos.json` (12): aula luminosa sin personas para la portada; cuatro rincones por edades (bebés, gateo, pintura,
manualidades); huerto escolar; patio, rincón de lectura, bloques de madera, comedor, psicomotricidad y sala de
siesta. Siempre sin personas, sin texto legible y sin logotipos. El equipo lleva la silueta `persona.svg`.

## Qué no hacer

- Volver a la caja centrada estrecha con tarjetas blancas o al hero de la base (dos columnas con la foto flotando).
- Meter dibujos de personajes o tipografías «infantiles» descargadas: la alegría la ponen el color, las formas y
  el ritmo de bandas.
- Parecerse a `veterinaria` (turquesa y coral, tarjetas redondeadas) o a `academia-formacion` (índigo y lima).
