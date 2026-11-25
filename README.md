# Ciudad Incremental · Análisis de transporte

**¿Dónde reubicar a las familias que viven en zonas de alto riesgo de Medellín, sin alejarlas de la ciudad?**

Este repositorio es el componente de transporte de **Ciudad Incremental: Infraestructura de riesgo, redes y vivienda para el reordenamiento territorial**, propuesta del frente de trabajo *Infraestructura para un país de ciudades* del Consejo de Jóvenes de la Cámara Colombiana de la Infraestructura (CCI), con la Universidad EAFIT.

<p align="center">
  <img src="Images/08_sitios_propuestos.png" alt="Mapa de Medellín con los barrios en riesgo en naranja y los sitios propuestos para reubicar a sus familias, coloreados según su nota" width="720">
  <br>
  <em>Resultado: los barrios en riesgo (naranja) y los sitios propuestos para cada uno, coloreados según su nota. La línea punteada une cada barrio con su sitio.</em>
</p>

**Contenido:** [La historia detrás](#la-historia-detrás) · [Cómo funciona](#cómo-funciona-paso-a-paso) · [Qué se obtiene](#qué-se-obtiene) · [Estructura del repositorio](#estructura-del-repositorio) · [Cómo usarlo](#cómo-usarlo) · [Datos](#de-dónde-salen-los-datos) · [Limitaciones](#lo-que-hay-que-tener-en-cuenta)

---

## La historia detrás

En Medellín hay familias que viven en laderas o a la orilla de quebradas donde el peligro de un deslizamiento o una inundación es tan grande que **ninguna obra lo puede resolver**. Para protegerlas, tienen que mudarse.

Casi siempre ocurre al revés de como debería: la gente llega primero, construye como puede, y años después el Estado intenta llevar agua, vías y obras. *Ciudad Incremental* propone **invertir ese orden**: preparar primero un terreno seguro, con servicios y vías, y llevar allí a las familias, con una vivienda que puedan ir ampliando con el tiempo.

Pero aparece una pregunta clave: **¿dónde debe quedar ese terreno?**

Muchos reasentamientos fallan porque las familias terminan en un lugar seguro pero **lejos de todo**: del trabajo, del colegio de los niños, del centro de salud, del metro. Una casa nueva no sirve de mucho si para llegar al trabajo hay que caminar una hora en subida.

Este análisis busca, **para cada barrio en riesgo**, un terreno que cumpla tres cosas:

1. **Que sea seguro** y que el plan de ordenamiento de la ciudad permita construir allí.
2. **Que quede cerca** del barrio de origen, para que las familias no pierdan su vida de siempre.
3. **Que desde allí se pueda llegar caminando** al transporte público, a la salud y al colegio, o que hacerlo posible no cueste demasiado.

> No busca el mejor terreno de toda la ciudad. Busca **el mejor terreno para cada barrio**.

---

## Cómo funciona, paso a paso

Imagina que tienes que ayudar a una familia a escoger un nuevo hogar. Harías más o menos esto:

### 1. Conocer el terreno
Se usa un **mapa de alturas** de la ciudad para saber qué tan empinado es cada lugar. En Medellín esto importa mucho: no es lo mismo caminar 500 metros en plano que 500 metros subiendo una loma.

![Altura y pendiente de Medellín y sus alrededores](Images/02_pendiente.png)
*Izquierda: altura sobre el nivel del mar. Derecha: pendiente. El valle es casi plano; las laderas oriental y occidental superan con facilidad el 30 %.*

### 2. Conocer las calles
Se descarga el mapa de todas las calles, andenes, senderos y escaleras de Medellín (de **OpenStreetMap**, un mapa libre hecho por voluntarios). Para cada tramo se calcula **cuánto se tarda una persona en recorrerlo**: en plano se camina a unos 5 km/h; subiendo una pendiente fuerte, a menos de la mitad.

### 3. Ubicar lo que la familia necesita cerca
Se ubican en el mapa las **estaciones del metro, metrocable, tranvía y Metroplús**, los **paraderos de bus**, los **centros de salud** y los **colegios**.

![Paraderos, colegios, centros de salud y estaciones del sistema masivo en Medellín](Images/03_destinos.png)
*3.667 paraderos, 998 colegios, 507 centros de salud y 77 estaciones del sistema masivo.*

### 4. Medir los minutos caminando
Para cada esquina de la ciudad se calcula **cuántos minutos se tarda en llegar caminando** a la estación, al paradero, al centro de salud y al colegio más cercanos, siempre por las calles y teniendo en cuenta las subidas.

Una forma de imaginarlo: se deja caer una gota de tinta en cada estación y la tinta avanza por las calles a la velocidad de una persona caminando. Cada esquina queda marcada con el minuto en que le llegó la tinta.

<p align="center">
  <img src="Images/04_minutos_caminando.png" alt="Mapa de minutos caminando hasta el sistema masivo: verde cerca de las líneas del metro, rojo en las laderas" width="520">
  <br>
  <em>Minutos caminando hasta el metro, cable, tranvía o Metroplús. Verde: menos de 10 minutos. Rojo: 45 o más, sobre todo en las laderas.</em>
</p>

### 5. Encontrar los barrios en riesgo
Con los mapas oficiales de la Alcaldía se ubican las **zonas de alto riesgo no mitigable**, donde la norma obliga a reasentar, y los barrios de origen informal que el plan de ordenamiento marca para **mejoramiento integral**. Para cada barrio se anota **cómo está conectado hoy**: cuántos minutos tiene, en el caso típico, hasta el metro, el bus, la salud y el colegio.

<p align="center">
  <img src="Images/05_barrios_en_riesgo.png" alt="Barrios en riesgo numerados de T1 a T33, coloreados según los minutos caminando hasta el sistema masivo hoy" width="520">
  <br>
  <em>Los territorios en riesgo (T1 a T33), coloreados según cuántos minutos caminan hoy hasta el sistema masivo.</em>
</p>

### 6. Descartar lo que no sirve
Se descarta el terreno donde **no se puede o no se debe construir**: zonas de amenaza alta, áreas protegidas, orillas de quebradas, terrenos demasiado empinados o lugares sin ningún camino cerca.

<p align="center">
  <img src="Images/06_terreno_descartado.png" alt="Mapa de Medellín en hexágonos que muestra por qué se descarta cada terreno: amenaza alta, POT, pendiente, suelo de protección o sirve" width="560">
  <br>
  <em>¿Dónde se puede construir? Cada hexágono muestra la razón por la que se descarta. Solo los de color arena sirven.</em>
</p>

### 7. Calificar cada terreno posible
Cada terreno que queda recibe una nota de 0 a 1 según cinco preguntas:

| Pregunta | Peso |
|---|---|
| **¿Cuánto cuesta conectarlo?** Qué obras faltan (una calle, un paradero, unas escaleras, una ruta de bus) para que el día de la mudanza haya un paradero a 10 minutos y el metro a 20 minutos | 30 % |
| **¿Las familias quedan igual o mejor que hoy?** No se vale reubicarlas peor conectadas que donde viven | 20 % |
| **¿Queda cerca del barrio?** Para no romper su vida de siempre | 20 % |
| **¿A cuántos vecinos les sirven esas obras?** Si se construye una escalera o un paradero, también lo usa el barrio de al lado | 20 % |
| **¿Qué tan empinado es?** Construir en plano es más fácil y barato | 10 % |

![Dos de los cinco criterios en el mapa: qué tan fácil es conectar cada terreno y cuántos vecinos se benefician](Images/07_calificacion.png)
*Dos de las cinco preguntas en el mapa. Izquierda: qué tan fácil es conectar cada terreno (1 = ya cumple el mínimo). Derecha: a cuántos vecinos en riesgo les sirven las obras.*

### 8. Proponer los mejores sitios
Para cada barrio se proponen **los dos mejores sitios**, cada uno con una **ficha** que dice qué obras de transporte hacen falta para que las familias queden bien conectadas desde el primer día.

### 9. Revisar que el resultado sea confiable
Los pesos de la tabla anterior son una decisión del equipo. Para comprobar que los sitios no dependen de esa decisión, el análisis se repite **500 veces con pesos un poco distintos** y se mide qué tan seguido cada sitio sigue saliendo bien.

---

## Qué se obtiene

En la carpeta `resultados/`:

| Archivo | Qué es |
|---|---|
| `mapa_barrios_y_sitios.png` | Mapa con los barrios en riesgo y los sitios propuestos, listo para un informe |
| `mapa_barrios_y_sitios.html` | El mismo mapa, interactivo: se abre en el navegador y se puede hacer clic en cada sitio |
| `sitios_por_barrio.csv` | Tabla con cada sitio, su nota y las obras que necesita (se abre en Excel) |
| `ciudad_incremental_transporte.gpkg` | Todas las capas para revisar en QGIS |
| `red_y_destinos.gpkg` | La red de calles con los minutos de cada esquina y los destinos, para QGIS |

---

## Estructura del repositorio

```
Ciudad-Incremental-analisis-de-transporte/
├── ciudad_incremental_transporte_medellin.ipynb   # El análisis completo, paso a paso
├── README.md                                      # Este archivo
├── requirements.txt                               # Librerías de Python
├── .gitignore                                     # Lo que no se sube (datos pesados y resultados)
├── Images/                                        # Figuras de este README
│   ├── 02_pendiente.png
│   ├── 03_destinos.png
│   ├── 04_minutos_caminando.png
│   ├── 05_barrios_en_riesgo.png
│   ├── 06_terreno_descartado.png
│   ├── 07_calificacion.png
│   └── 08_sitios_propuestos.png
├── datos/
│   ├── LEEME.md                                   # Qué poner aquí y qué se crea solo
│   ├── output_be.tif                              # Mapa de alturas: se pone a mano (no está en GitHub)
│   ├── pot/                                       # Mapas de la Alcaldía (se descargan solos)
│   └── cache/                                     # Recortes, pendientes y red de calles (se crean solos)
├── cache/                                         # Respuestas guardadas de OpenStreetMap (se crea sola)
└── resultados/                                    # Mapas, tabla y capas para QGIS (se crea sola)
```

Solo el notebook, la documentación y las figuras están en GitHub. Todo lo demás se descarga o se calcula al ejecutar el notebook.

---

## Cómo usarlo

**1. Instala Python** (se recomienda [Anaconda](https://www.anaconda.com/download), que ya trae Jupyter).

**2. Instala las librerías.** Abre una terminal en esta carpeta y escribe:

```bash
pip install -r requirements.txt
```

**3. Agrega el mapa de alturas.** Copia el archivo `output_be.tif` en la carpeta `datos/` (ver `datos/LEEME.md`). Es el único archivo que hay que poner a mano; no está en el repositorio porque pesa demasiado.

**4. Abre el notebook** `ciudad_incremental_transporte_medellin.ipynb` en Jupyter o en VS Code y ejecuta las celdas **en orden**, de arriba hacia abajo.

La primera vez tarda varios minutos, porque descarga los mapas de la Alcaldía y las calles de OpenStreetMap. Las siguientes veces es mucho más rápido, porque todo queda guardado en `datos/`.

Cada paso del notebook tiene una explicación en lenguaje sencillo. **No es necesario saber programar para seguirlo.**

---

## De dónde salen los datos

| Dato | Fuente |
|---|---|
| Mapa de alturas (modelo digital de elevaciones, 30 m) | Archivo `output_be.tif` |
| Calles, andenes, senderos, escaleras, centros de salud y colegios | [OpenStreetMap](https://www.openstreetmap.org) |
| Amenaza y riesgo (deslizamientos, inundaciones, avenidas torrenciales), áreas protegidas, retiros, humedales y tratamientos urbanísticos | Alcaldía de Medellín, POT Acuerdo 48 de 2014 ([servicios de mapas](https://www.medellin.gov.co/servidormapas/rest/services)) |
| Estaciones del metro, metrocable, tranvía y Metroplús | Alcaldía de Medellín |
| Paradas de bus autorizadas | Alcaldía de Medellín, Secretaría de Movilidad |

Los mapas de la Alcaldía y las calles se descargan automáticamente al ejecutar el notebook.

---

## Lo que hay que tener en cuenta

- **Los mapas oficiales son los del POT de 2014.** En 2026 el Concejo aprobó una revisión del POT con nuevos mapas de amenaza; cuando se publiquen, hay que actualizar el análisis.
- **OpenStreetMap no es perfecto.** En las laderas pueden faltar escaleras y caminos. Los sitios propuestos deben revisarse en campo.
- **Estar cerca no es lo mismo que tener buen servicio.** Un paradero cerca con un bus cada hora no es buen acceso. La frecuencia de los buses aún no está incluida.
- **Los costos de las obras son relativos.** Sirven para comparar sitios entre sí, no son un presupuesto.
- **Las reglas y los pesos son una propuesta.** Están todos en un mismo lugar del notebook (la celda *Parámetros*), para que el equipo pueda discutirlos y cambiarlos.

---

## Créditos

**Proyecto:** Ciudad Incremental: Infraestructura de riesgo, redes y vivienda para el reordenamiento territorial
**Frente de trabajo:** Infraestructura para un país de ciudades · Consejo de Jóvenes de la Cámara Colombiana de la Infraestructura (CCI)
**Autor de la idea original y del análisis de transporte:** Santiago Ayala Martínez, Universidad EAFIT

Datos: © colaboradores de OpenStreetMap (licencia ODbL) · Alcaldía de Medellín.
