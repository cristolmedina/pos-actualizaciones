# Dos negocios en la misma caja

Instrucciones completas para trabajar dos negocios independientes —por ejemplo un **detal** y un
**mayoreo**— en el mismo computador, con la misma impresora y la misma báscula.

> **Es un caso especial.** Si el local tiene un solo negocio, no haga nada de esto: todo sigue
> funcionando como siempre.

Hace falta la versión **1.2.33 o posterior** en la caja. La versión se ve en Administración →
Acerca de.

---

## Cómo queda

| | Detal | Mayoreo |
|---|---|---|
| Cómo se entra | El acceso directo de siempre (`http://localhost:8080`) | `http://127.0.0.1:8080/mayoreo` (otra sesión del navegador) |
| Productos, precios, inventario | Los suyos | Los suyos |
| Clientes, cartera, proveedores | Los suyos | Los suyos |
| Caja, turnos, arqueos | Su terminal | Su terminal |
| Numeración de recibos y reportes | La suya | La suya |
| Impresora | La misma, con su llave | La misma, con su llave |
| Báscula | La misma; se la pasan | La misma; se la pasan |

**Los dos negocios no comparten datos.** Lo único común es el computador, la impresora y la báscula.

---

## Paso 1 · Crear el negocio de mayoreo

1. En el computador de la caja abra el navegador en:

   ```text
   http://localhost:8080/plataforma
   ```

2. Entre con el usuario de la consola (`admin`) y su clave. Es la que venía en
   `C:\POS\PRIMER-INGRESO.txt` la primera vez, ya cambiada por usted.
3. Toque **«+ Nuevo negocio»** y llene:
   - **Nombre comercial:** el que verá en pantalla y en los recibos, por ejemplo «Mayoreo El
     Portal».
   - **Dirección de acceso:** `mayoreo` (minúsculas, sin espacios ni tildes). Es la que va en la
     dirección: `…/mayoreo`.
   - **Tipo de negocio:** **Distribución**.
   - **Cómo va a funcionar:** encienda lo que vaya a usar (cartera, despachos, etc.).
   - **Su administrador:** usuario, nombre, correo y una clave inicial. Anótelos: con ellos se
     entra al mayoreo.
4. Toque **«Crear negocio»**. El negocio nace con su caja (terminal «Caja 1»), su bodega, sus medios
   de pago, sus roles y sus categorías de gasto.
5. Salga de la consola.

---

## Paso 2 · Abrir el mayoreo en su propia sesión

El navegador guarda una sesión por dirección. Para que el detal y el mayoreo no se pisen, cada uno
se abre por una dirección distinta:

- **Detal:** el acceso directo del escritorio, como siempre (`localhost`).
- **Mayoreo:** escriba en el navegador

  ```text
  http://127.0.0.1:8080/mayoreo
  ```

  (es la misma caja, con `127.0.0.1` en vez de `localhost`).

Para no escribirlo cada vez, cree un acceso directo en el escritorio: clic derecho en el escritorio →
**Nuevo → Acceso directo**, pegue esa dirección y llámelo «Mayoreo».

> **Otra forma:** abrir el mayoreo en otro perfil de Chrome o Edge, con la dirección
> `http://localhost:8080/mayoreo`. Funciona igual. Lo que **no** hay que hacer es abrir los dos
> negocios en pestañas del mismo perfil con la misma dirección (`localhost`): ahí comparten la
> sesión y se cierran el uno al otro.

Cada sesión recuerda su negocio. Si alguna vez la caja pregunta **«¿A qué negocio entra?»**, elija el
que corresponde a esa ventana y no vuelve a preguntar.

---

## Paso 3 · Entrar y enrolar la terminal del mayoreo

Una terminal es la caja registradora del negocio. Cada negocio tiene la suya, y enrolarla deja ese
computador autorizado para abrir caja y cobrar.

1. En la ventana del mayoreo (`127.0.0.1:8080/mayoreo`), entre con el administrador del Paso 1. El
   sistema le pide cambiar la clave.
2. Vaya a **Administración → Terminales**. Ya hay una, «Caja 1», **Sin enrolar**.
3. En su renglón toque **«Código de activación»**. Aparece un código: sirve una sola vez y caduca.
   Cópielo o anótelo.
4. Salga (cerrar sesión). En la pantalla de ingreso del mayoreo dice **«Equipo no enrolado: Enrolar
   terminal»**. Tóquelo.
5. Escriba el **código de activación** y toque **«Enrolar»**. Debe decir **«Terminal enrolada»**.
6. Entre de nuevo. Abajo del formulario de ingreso ahora dice **«✓ Terminal enrolada en este
   equipo»**.

La caja guarda una copia de esa credencial en el disco, **una por negocio**: enrolar el mayoreo no
toca la del detal. Si un limpiador de Windows borra el navegador, cada negocio recupera la suya.

> El detal **no** se vuelve a enrolar. Ya lo está.

---

## Paso 4 · Cargar lo del mayoreo

Es un negocio aparte, así que no ve nada del detal. Antes de vender, en el mayoreo:

1. **Datos del negocio** (Administración → Datos del negocio): razón social, NIT, dirección.
   Salen en los recibos del mayoreo.
2. **Productos y precios** (Administración → Productos, o Cargar productos desde Excel).
3. **Usuarios y PINs** (Administración → Usuarios) para quienes van a vender en el mayoreo.
4. **Inventario inicial:** Inventario → Entrada manual, o Compras → Recibir mercancía.

---

## Paso 5 · La impresora para los dos negocios

La térmica es una sola. El programa que imprime (el **agente**) le pregunta a cada negocio, con una
llave de cada uno, si hay algo por imprimir, y lo imprime en orden. Un negocio nunca ve ni imprime
los papeles del otro.

### 5.1 · Crear la llave del mayoreo

1. En la ventana del **mayoreo**: **Administración → Conexiones → Llaves de la API**.
2. En **«Para qué es»** escriba `Agente de impresión`.
3. Marque **«Agente de impresión de la caja»** (y nada más).
4. Toque **«Crear llave»**. Aparece una llave que empieza por `pos_live_`. **Se muestra una sola
   vez:** toque **«Copiar»** y péguela en un Bloc de notas. Después toque **«Ya lo guardé»**.

### 5.2 · Ponerla en el archivo del agente

1. Abra la carpeta `C:\POS\configuracion\`.
2. Abra **`agente.properties`** con el Bloc de notas (clic derecho → Abrir con → Bloc de notas).
   Si no existe, copie `agente.properties.ejemplo` y llámelo `agente.properties`.
3. Ya tiene la línea del detal, que empieza por `llave=`. **No la toque.** Debajo, agregue la del
   mayoreo empezando por `llave.mayoreo=`:

   ```properties
   servidor=http://localhost:8080
   llave=pos_live_AAAAAAAA_la_del_detal_que_ya_estaba
   llave.mayoreo=pos_live_BBBBBBBB_la_que_acaba_de_copiar
   ```

   Reglas del archivo:
   - Una llave por línea, sin espacios antes ni después del `=`.
   - La del detal sigue en `llave=`. La del mayoreo va en `llave.` + un nombre cualquiera
     (`llave.mayoreo=`).
   - Las líneas que empiezan por `#` son comentarios y no hacen nada.
4. Guarde el archivo (Archivo → Guardar). Si el Bloc de notas pregunta la codificación, deje
   **UTF-8**.

### 5.3 · Reiniciar el agente

El agente lee el archivo al arrancar. **Reinicie el computador**, o cierre el POS y vuelva a abrirlo
con el acceso directo.

### 5.4 · Configurar la impresora en el mayoreo

1. En la ventana del **mayoreo**: **Administración → Impresoras**. Arriba debe aparecer el agente
   del equipo reportando. Si dice «Ningún agente ha reportado desde este local», revise el Paso 5.2.
2. Toque **«Agregar impresora»** y llene:
   - **Cómo se conecta:** Windows (o Red, si la térmica es de red).
   - **Impresora:** elija de la lista **la misma** que usa el detal (el agente reporta las que ve
     Windows).
   - **Ancho del papel / Columnas:** los mismos que tiene el detal.
   - **Qué papeles salen por aquí:** Recibo de venta, Cierre de caja y los que use.
   - **Corta el papel / Abre el cajón:** como en el detal.
3. Guarde.

### 5.5 · Probar

Haga una venta de prueba en **cada** negocio. Cada recibo debe salir con los datos de su negocio.
Si alguno no sale, mire el registro del agente en `C:\POS\datos\registros\agente.log`:

- `negocios: 2` al arrancar → leyó las dos llaves.
- `El servidor rechazo la llave …` → esa llave está mal copiada o se revocó: créela otra vez
  (Paso 5.1) y reemplácela.

---

## Paso 6 · La báscula

La báscula la puede tener abierta **una sola ventana a la vez**.

1. **La primera vez en cada ventana**: con el parámetro de la báscula encendido (Administración →
   Parámetros, «Bascula conectada al equipo»), toque **«⚖ conectar»** y elija el puerto de la báscula
   en el diálogo del navegador. El navegador lo recuerda.
2. **Pasarla al otro negocio:** en la ventana que la necesita aparece **«⚖ la tiene detal ·
   pedirla»** (o «la tiene mayoreo»). Tóquelo: en unos segundos la otra ventana la suelta y esta la
   abre sola.
3. **Soltarla a mano:** toque **«⚖ conectada»** y confirme.

Si una ventana se cerró con la báscula tomada, a los 10 segundos queda libre para la otra.

---

## ¿Se pueden mezclar?

No, por diseño:

- **Los datos.** Cada fila de la base lleva su negocio, y la base misma impide que un negocio lea o
  escriba los datos del otro (aislamiento por negocio en PostgreSQL, el mismo que separa a todos los
  clientes en la nube).
- **La sesión.** Cada negocio entra por una dirección distinta del navegador (`localhost` y
  `127.0.0.1`), y el navegador las guarda por separado: la sesión, la terminal y las ventas
  pendientes sin conexión de una no las ve la otra.
- **La terminal.** Cada negocio tiene la suya y su propia copia en disco
  (`terminal-de-la-caja-<negocio>.properties`).
- **La impresión.** Cada llave reclama solo los trabajos de su negocio. El agente los imprime uno
  tras otro, así que no se cruzan dos papeles.
- **La caja.** Turnos, arqueos, gastos y numeración son de cada negocio.

Lo que **sí es común**, y está bien que lo sea: el computador, la base de datos (un solo respaldo
guarda los dos negocios), las actualizaciones del POS y el usuario de la consola.

### Lo que hay que saber

1. **No abra los dos negocios en el mismo perfil con la misma dirección.** Es la única forma de que
   se pisen las sesiones (Paso 2).
2. **Si el mayoreo le vende al detal**, no pasa solo de un negocio al otro: es una venta en el
   mayoreo y una compra (Recibir mercancía) en el detal.
3. **La copia en la nube** todavía no está en uso. Cuando se active, la sincronización trabaja con
   **un solo negocio por equipo**: habrá que decidir cuál de los dos se copia, o ampliarla.
4. **La báscula y la impresora compartidas** no se pudieron probar con el equipo real al escribir
   esto. Haga la venta de prueba del Paso 5.5 y una pesada en cada negocio el primer día.

---

## Si algo no funciona

| Qué pasa | Qué hacer |
|---|---|
| El acceso directo pregunta «¿A qué negocio entra?» | Elija el detal. No vuelve a preguntar en esa sesión. |
| El acceso directo entra al mayoreo | En la pantalla de ingreso, cambie la dirección a `localhost:8080/` + la del detal. A partir de ahí recuerda el detal. |
| «Equipo no enrolado» en un negocio | Genere un código nuevo en Administración → Terminales de **ese** negocio y enrólelo (Paso 3). |
| No imprime uno de los dos | Revise su línea en `agente.properties` y reinicie el equipo (Paso 5). Mire `agente.log`. |
| No imprime ninguno | El agente no arrancó: revise que el archivo se llame exactamente `agente.properties` y que tenga `llave=`. |
| La báscula no pasa | Toque «⚖ conectada» en la otra ventana para soltarla, y «⚖ conectar» en esta. |
