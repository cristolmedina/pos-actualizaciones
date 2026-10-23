# Actualizaciones del POS

Aquí solo hay **paquetes compilados** de la caja local. El código está en otro repositorio, que es
privado.

Cada versión es un *release* con tres archivos:

- `POS-Instalador-<versión>.exe`: el instalador para un equipo nuevo.
- `pos-<versión>.zip`: el paquete que bajan las cajas que ya están instaladas.
- `manifest.properties`: la versión, la suma del paquete y su firma.

Las cajas miran `releases/latest/download/manifest.properties` cada pocas horas. Si la versión es
mayor que la suya, bajan el paquete, **comprueban la firma** con la llave pública que traen
adentro, y lo instalan al próximo arranque. Un paquete sin firma válida no se instala.

Los releases los publica la acción del repositorio de código al crear un tag `v*`. No se suben a
mano.
