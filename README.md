# Tarea 09

## Asignatura

- SXE

## Alumno

- Anxo Vázquez Lorenzo - 2 DAM

## Proyecto

### `compose.yml` y `.env`

Copio en un archivo `compose.yml` el ejemplo de la tarea y en mi archivo `.env` defino las siguientes variables (`.env.example`):

```
ODOO_TAG
ODOO_PORT
POSTGRES_USER
POSTGRES_PASSWORD
PGADMIN_EMAIL
PGADMIN_PASSWORD
```

### `config/odoo.conf`

Creo una carpeta llamada `config` con un archivo `odoo.conf` que será usado por el contenedor de `odoo`.


`Compose`: 

```
volumes:
      - odoo-data:/var/lib/odoo
      - ./config:/etc/odoo
      - ./addons:/mnt/extra-addons

```

### Contraseña admin odoo

Para que funcione se necesita establecer en el campo `admin_passwd` una contraseña (archivo `odoo.conf`) el cual viene vacío.


## Despliegue con `Demo Data`

Despliego con `docker compose up -d` y pruebo a acceder, una vez dentro indico la casilla `Demo Data`, le doy a `Create Database` y espero a que termine.

![formulario-demo-data](./imgs/formulario_inicial.png)


Una vez terminado instalo las aplicaciones `Contactos, Ventas, Facturación e Inventario`.

![app](./imgs/apps.png)

Una vez instalados miro qué productos estoy vendiendo (los que me puso automáticamente con `Demo Data`):

![productos](./imgs/productos.png)

## Bases de datos

Creo las siguientes bases de datos:

- `db` -> base de datos con datos de prueba

- `db2` -> base de datos vacía.

Al acceder por primera vez me deja crear una base de datos que, una vez creada, accedo a `http://localhost:8069/web/database/manager` y creo otra base de datos (sin `Demo Data`).

![db1-2](./imgs/dbs.png)

Una vez creadas las bases de datos las compruebo desde `PgAdmin`:

![pgadmin](./imgs/pgadmin.gif)


## Ejercicio 1

Escojo un producto del tipo `Bienes` y miro su ficha:

![prodbienes](./imgs/prodbienes.png)

Ahora otro del tipo `Servicio`:

![serviciotipo](./imgs/prodservicio.png)

Miro las propiedades de uno de los productos y relleno algunos de sus datos:

![producto](./imgs/productoejemplo.gif)


## Ejercicio 2

### (I -II) Contactos

Creo los siguientes registros:

![compañía](./imgs/contacto-compañía.png)

![persona](./imgs/contacto-persona.png)

Creo la etiqueta cliente y añado el siguiente cliente:

![cliente](./imgs/clientenuevo.png)


### (III) Productos

Creo los productos indicados:

![servicio](./imgs/Servicio.png)

![bien](./imgs/librotec.png)

Para especificar la marca en ambos casos lo hago de la siguiente forma:

![marca](./imgs/marca.png)

### (IV) Ventas

![presupuesto](./imgs/presupuesto.png)

Le doy a enviar y dejo el diseño del documento por defecto, al terminar de enviarlo miro que el pedido se ha creado correctamente.

![pedido-venta](./imgs/pedidoventa.png)

### (V - VI) Facturación


Desde el pedido le doy a `Crear Factura` y selecciono `Factura normal`. Le doy a pagar y uso la cuenta bancaria de prueba falsa que me da odoo.

![pago](./imgs/pagado.png)

Al compararla con una factura a compañía la principal diferencia es en la sección de cliente, si es para una persona pone su nombre y compañía, en caso contrario sólo la compañía.

### (VII) Chatter

Para programar una actividad en la parte derecha le doy a Actividad y programo una llamada:

![llamada](./imgs/llamada.png)

## Ejercicio 3

Creo el siguiente filtro y lo agrego como favorito.

![filtro](./imgs/filtro.png)

## Ejercicio 4

### Activar modo desarrollador

Activo el modo desarrollador desde los ajustes y compruebo que aparece el escarabajo arriba a la derecha.

### Contacto

Para ver nombre nombres técnicos como de campos como `NIF` o sus `etiquetas` paso el ratón por encima:

![contacto](./imgs/devmodecontacto.gif)

### Factura

Hago lo mismo que en el paso anterior pero sobre una factura:

![factura](./imgs/devmodefactura.gif)

## Incidencias


| Fecha | Síntoma | Causa y solución |
| --- | --- | --- |
| 09/11/26 | Productos y facturas en dólares | Como no me dejó cambiar la divisa directamente en `Configuración->Ajustes->Moneda`, la solución más sencilla era usar dos divisas y, en las facturas, decidir qué divisa usar para cada una de ellas. |
| 10/11/26 | `admin_passwd` de Odoo directamente en `odoo.conf`| Decidí simplemente dejar el campo en `odoo.conf` en blanco para subirlo al repositorio (mira la declaración de `IA`). |

## Bibliografía y Declaración de IA

- Gemini - `admin_passwd` de `odoo.conf`

      Prompt: ¿Existe alguna variable de entorno en la imagen de odoo que me permita establecer la contraseña de admin, la admin_passwd=123456 de odoo.conf?

      Conclusión: Su respuesta fue que no, pero que lo podía hacer poniendo `command: --admin-passwd=123456` en en `compose.yml`, lo cual era completamente inventado y no existía, así que decidí simplemente dejar el campo en `odoo.conf` en blanco para subirlo al repositorio

- Gemini - Tabla markdown

      Prompt: Arreglame esta tabla en markdown (adjuntada tabla original)

      Conclusión: le adjunté la tabla original para que la arreglase y se pudiese ver correctamente en la `preview` de `github`, como tal no se modificó el valor de los campos sólo el como creaba en el `Readme` (me faltó poner `| --- | --- | --- |`)

- Dockerhub - Imagen oficial de docker

      https://hub.docker.com/_/odoo