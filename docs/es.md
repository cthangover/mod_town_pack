# Town Pack — fondos de la ciudad, la casa y el bar con ambiente sonoro

Town Pack es escenografía lista para usar en una historia ambientada en una ciudad pequeña. Trae tres fondos ilustrados —una esquina en la entrada de la ciudad, el recibidor de una casa y un bar nocturno— y el sonido ambiente en bucle del bar. No incluye historia, escenas ni personajes: cada juego decide dónde mostrar las imágenes.

Dos juegos integrados ya lo comparten. **Cthangover** usa la entrada de la ciudad y el recibidor; la plantilla **My Novel**, los tres fondos y el ambiente del bar. Como ambos juegos toman los mismos archivos de este mod, cualquier arreglo o imagen mejorada en Town Pack llega a los dos.

## Qué contiene

La entrada de la ciudad, `town/town_entry`: una esquina adoquinada con toldos de colores en las tiendas.

![Fondo de la entrada de la ciudad: un edificio en una esquina con toldos verdes y blancos en una calle adoquinada.](assets/town_entry.jpg)

El recibidor de la casa, `home/vestibule`: un vestíbulo con escalera, un sillón y un cuadro.

![Fondo del recibidor: una escalera de madera, un sillón, un banco y un cuadro enmarcado en un vestíbulo de luz cálida.](assets/vestibule.jpg)

El bar, `bar/bar`: mesas con faroles, una barra y estanterías con botellas.

![Fondo del bar: mesas iluminadas por faroles, la barra y estanterías con botellas bajo un techo de vigas.](assets/bar.jpg)

El ambiente del bar, `bar/bar_ambient`: un bucle Ogg Vorbis con el ambiente del bar para el canal de sonido Ambience.

Las tres imágenes miden 1920 × 1024. Cada una tiene un archivo complementario en escala de grises con el mismo nombre y el sufijo `_depth`:

![La imagen de profundidad de la entrada de la ciudad: la misma composición en escala de grises.](assets/town_entry_depth.jpg)

Una imagen de profundidad no se ve directamente. Al mostrar un fondo, el juego también carga `<name>_depth` y se lo pasa al sistema de iluminación, que lo usa para las luces colocadas sobre la escena. Un fondo sin su imagen de profundidad se muestra igual con normalidad.

## Dónde lo verás

- **Cthangover:** la escena `town_entry` (la entrada de la ciudad) y la escena `home_vestibule`.
- **Plantilla My Novel:** `my_novel_town`, `my_novel_home` y `my_novel_bar`. La escena del bar también reproduce `bar/bar_ambient`.

La misma entrada de la ciudad en la plantilla My Novel, donde abre el juego con una línea de narración:

![Primera escena de My Novel: el fondo de la entrada de la ciudad tras la línea «La ciudad al anochecer. Las farolas ya están encendidas y una corriente fresca recorre los adoquines».](assets/reuse-my-novel.jpg)

Y en Cthangover, donde otra historia ofrece sus propias opciones sobre la misma imagen:

![La entrada de la ciudad en Cthangover: el mismo fondo con las opciones «Volver a casa» y «Revisar el callejón».](assets/reuse-cthangover.jpg)

Town Pack forma parte de las colecciones de ambos juegos y se carga con ellos. Instalarlo no añade estos lugares a un juego cualquiera: tiene que ser el juego quien use los fondos en sus propias escenas.

## Usa los fondos en tu juego

1. Añade `town_pack>=1` a la lista `depends` de tu mod de contenido.
2. Añade `town_pack>=1` a la colección de tu juego, como hace la plantilla My Novel en su bloque **Assets**.
3. Refiérete a los recursos por su nombre. Los nombres son relativos a `backgrounds/` y `sounds/` y no llevan extensión.

```jsonc
// mods/my_game/manifest.json — añádelo a la lista existente
"depends": ["town_pack>=1"]
```

Una escena que muestra el bar y reproduce su ambiente, tomada de la escena `my_novel_bar` de la plantilla:

```json
{
  "name": "my_bar",
  "defaultBackground": "bar/bar",
  "defaultAmbient": "bar/bar_ambient"
}
```

Un escenario también puede cambiar la imagen durante un diálogo:

```scenario
background town/town_entry
text "A estas horas la calle está vacía."
```

Los nombres disponibles son:

```text
town/town_entry     backgrounds/town/town_entry.png
home/vestibule      backgrounds/home/vestibule.png
bar/bar             backgrounds/bar/bar.png
bar/bar_ambient     sounds/bar/bar_ambient.ogg
```

## Cambia una imagen para tu juego

Para cambiar una imagen sin tocar Town Pack, incluye en tu propio mod un archivo con el mismo nombre relativo, por ejemplo `backgrounds/bar/bar.png`, y declara `town_pack>=1` en su `depends`. El mod que depende del propietario se carga después y gana. Si sustituyes un fondo, incluye también su archivo `_depth` con el mismo nombre: si no, el juego seguirá encontrando la imagen de profundidad original de Town Pack y las luces seguirán la composición de la imagen antigua.

Sin la dependencia, dos mods que ofrezcan el mismo nombre no tienen un orden definido; la herramienta de mapa de recursos lo informa como error.

## Si falta algo

1. Un fondo negro o ausente suele indicar un nombre mal escrito. Los nombres distinguen mayúsculas de minúsculas y usan `/`.
2. Comprueba que Town Pack esté incluido en el juego que has lanzado, no solo instalado.
3. Sin sonido en el bar: comprueba que el `defaultAmbient` de la escena sea `bar/bar_ambient` y que el canal **Ambience** esté activado en **Settings → Sound**. La reproducción de sonido la ofrece el mod Audio Engine.
