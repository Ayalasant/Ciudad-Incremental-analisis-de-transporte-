# Carpeta de datos

## Lo que tienes que poner aquí

**`output_be.tif`**: el mapa de alturas de la zona (modelo digital de elevaciones).

Debe quedar directamente en esta carpeta, así:

```
datos/
├── output_be.tif     ← aquí
├── pot/              (la crea el notebook)
└── cache/            (la crea el notebook)
```

Características del archivo que se usó:
- Resolución de unos 30 metros.
- Sistema de coordenadas SIRGAS 2000 (EPSG:4674); el notebook también acepta otros sistemas.
- Cubre buena parte de Antioquia; el notebook recorta solo la zona de Medellín.

No está en el repositorio porque pesa unos 230 MB y GitHub no acepta archivos de más de 100 MB.

## Lo que se crea solo

- **`pot/`**: los mapas oficiales de la Alcaldía de Medellín (amenaza, riesgo, áreas protegidas, tratamientos, estaciones y paraderos). Se descargan la primera vez que ejecutas el notebook.
- **`cache/`**: archivos intermedios (el recorte del mapa de alturas, las pendientes y la red de calles), para que las siguientes ejecuciones sean rápidas.

Ninguna de estas dos carpetas se sube a GitHub. Si quieres volver a descargar todo desde cero, bórralas.
