# API Fake con JSON Server

## 1. Descripción del proyecto

Este proyecto permite crear una API REST falsa utilizando **JSON Server**, una herramienta de Node.js que transforma un archivo JSON en una API que podemos consultar desde el navegador o consumir desde una aplicación con JavaScript.

Es útil para practicar solicitudes HTTP, consultar información y realizar operaciones CRUD sin necesidad de crear un backend desde cero ni conectar una base de datos real.

## 2. Requisitos previos

Antes de comenzar, debemos tener instalados los siguientes programas:

- **Node.js:** permite ejecutar JavaScript fuera del navegador.
- **npm:** administrador de paquetes que se instala junto con Node.js.
- **Visual Studio Code:** editor de código recomendado para crear y modificar los archivos del proyecto.

Para verificar que Node.js y npm estén instalados, ejecutamos los siguientes comandos en la terminal:

```bash
node -v
npm -v
```

Si ambos comandos muestran un número de versión, podemos continuar.

## 3. Crear el proyecto

### Paso 1. Crear la carpeta

```bash
mkdir api-fake
```

Este comando crea una carpeta llamada `api-fake`.

### Paso 2. Ingresar a la carpeta

```bash
cd api-fake
```

Nos ubicamos dentro de la carpeta del proyecto para ejecutar los siguientes comandos.

### Paso 3. Inicializar npm

```bash
npm init -y
```

Este comando crea el archivo `package.json`, donde se almacena la información del proyecto y sus dependencias.

El parámetro `-y` acepta automáticamente las opciones predeterminadas de la inicialización.

## 4. Instalar JSON Server

Ejecutamos el siguiente comando:

```bash
npm install -D json-server
```

Este comando instala JSON Server como una dependencia de desarrollo del proyecto.

**Significado de los parámetros:**

- `npm install`: instala un paquete.
- `-D`: abreviatura de `--save-dev`; registra el paquete como dependencia de desarrollo.
- `json-server`: nombre de la herramienta que permite crear nuestra API Fake.

La instalación local permite que el proyecto tenga su propia versión de JSON Server, sin necesidad de instalarla globalmente en el computador.

## 5. Crear la base de datos falsa

En la raíz del proyecto, creamos un archivo llamado `db.json`.

Este archivo almacenará los datos que JSON Server expondrá mediante los endpoints.

Ejemplo de contenido:

```json
{
  "usuarios": [
    {
      "id": 1,
      "nombre": "Juan Pérez",
      "correo": "juan@example.com"
    },
    {
      "id": 2,
      "nombre": "María López",
      "correo": "maria@example.com"
    }
  ],
  "destinos": [
    {
      "id": 1,
      "nombre": "Cartagena",
      "departamento": "Bolívar"
    },
    {
      "id": 2,
      "nombre": "Guatapé",
      "departamento": "Antioquia"
    },
    {
      "id": 3,
      "nombre": "Salento",
      "departamento": "Quindío"
    }
  ]
}
```

**Importante:** el contenido debe ser JSON válido. Debemos utilizar comillas dobles en las propiedades y los textos, evitar las comas sobrantes y guardar el archivo después de modificarlo.

## 6. Estructura del proyecto

Después de realizar la instalación, la estructura básica será la siguiente:

```text
api-fake/
├── node_modules/
├── db.json
├── package.json
├── package-lock.json
└── README.md
```

- `node_modules/`: contiene los paquetes instalados.
- `db.json`: almacena los datos de nuestra API Fake.
- `package.json`: contiene la información y las dependencias del proyecto.
- `package-lock.json`: registra las versiones concretas de las dependencias instaladas.
- `README.md`: documenta el proyecto y explica cómo utilizarlo.

## 7. Ejecutar el servidor

Desde la terminal, dentro de la carpeta `api-fake`, ejecutamos:

```bash
npx json-server db.json
```

Este comando inicia JSON Server utilizando los datos del archivo `db.json`.

En la configuración habitual, el servidor se ejecuta en:

```text
http://localhost:3000
```

Debemos mantener abierta la terminal mientras queramos utilizar la API. Para detener el servidor, presionamos `Ctrl + C`.

## 8. Crear y consultar endpoints

JSON Server crea automáticamente endpoints a partir de las propiedades principales del archivo `db.json`.

### Endpoint de usuarios

```text
http://localhost:3000/usuarios
```

Devuelve la lista de usuarios.

Para consultar un usuario específico:

```text
http://localhost:3000/usuarios/1
```

### Endpoint de destinos

```text
http://localhost:3000/destinos
```

Devuelve la lista de destinos turísticos.

Para consultar un destino específico:

```text
http://localhost:3000/destinos/2
```

### ¿Cómo crear otro endpoint?

Para crear otro endpoint, agregamos una nueva colección en el archivo `db.json`.

Por ejemplo:

```json
{
  "productos": [
    {
      "id": 1,
      "nombre": "Mochila",
      "precio": 80000
    }
  ]
}
```

Este fragmento es solo un ejemplo de una colección nueva. Si queremos conservar los usuarios y destinos existentes, debemos agregar `"productos"` dentro del mismo objeto JSON, junto a las colecciones anteriores, en lugar de reemplazar todo el archivo.

El endpoint resultante será:

```text
http://localhost:3000/productos
```

Guardamos los cambios y comprobamos el endpoint en el navegador. JSON Server normalmente detecta las modificaciones del archivo automáticamente.

## 9. Comandos principales

| Comando | Función |
|---|---|
| `node -v` | Consulta la versión de Node.js. |
| `npm -v` | Consulta la versión de npm. |
| `mkdir api-fake` | Crea la carpeta del proyecto. |
| `cd api-fake` | Ingresa a la carpeta. |
| `npm init -y` | Inicializa el proyecto npm. |
| `npm install -D json-server` | Instala JSON Server localmente. |
| `npx json-server db.json` | Inicia la API Fake. |
| `Ctrl + C` | Detiene el servidor. |

### Instalación global (alternativa)

También existe la opción de instalar JSON Server globalmente:

```bash
npm install -g json-server
```

El parámetro `-g` significa instalación global, lo que permite utilizar el comando instalado desde distintas carpetas del computador.

Para comenzar, se recomienda la instalación local con `-D`, ya que deja registrada la dependencia dentro del proyecto.

## 10. Operaciones CRUD

JSON Server permite practicar operaciones CRUD mediante solicitudes HTTP, según la versión instalada:

| Operación | Método HTTP | Ejemplo |
|---|---|---|
| Consultar todos los usuarios | `GET` | `/usuarios` |
| Consultar un usuario | `GET` | `/usuarios/1` |
| Crear un usuario | `POST` | `/usuarios` |
| Actualizar un usuario | `PUT` o `PATCH` | `/usuarios/1` |
| Eliminar un usuario | `DELETE` | `/usuarios/1` |

El navegador permite consultar fácilmente los endpoints `GET`. Para probar `POST`, `PUT`, `PATCH` y `DELETE`, podemos utilizar herramientas como Postman o realizar solicitudes desde JavaScript con `fetch`.

**Nota:** el comportamiento exacto de las rutas y operaciones puede variar entre versiones de JSON Server.

## 11. Consideraciones importantes

- JSON Server es una herramienta de práctica; no reemplaza un backend real con autenticación, permisos y reglas de negocio.
- El archivo `db.json` actúa como fuente de datos y puede modificarse cuando se realizan operaciones de escritura compatibles.
- El servidor debe estar activo para que los endpoints respondan.
- Si el puerto 3000 está ocupado, debemos revisar el mensaje de la terminal y configurar otro puerto si es necesario.
- No debemos subir la carpeta `node_modules/` al repositorio; normalmente se incluye en `.gitignore`.

## 12. Objetivo de aprendizaje

Con este proyecto podemos aprender a:

- Comprender qué es una API REST.
- Identificar qué es un endpoint.
- Organizar información en formato JSON.
- Realizar solicitudes HTTP.
- Practicar operaciones CRUD.
- Consumir una API desde JavaScript.
- Preparar datos de prueba antes de desarrollar un backend real.

**Conclusión:** JSON Server nos permite practicar el consumo y funcionamiento básico de una API sin construir todavía un backend completo. Más adelante, estos conocimientos pueden aplicarse al conectar una interfaz web con un backend desarrollado en Spring Boot y una base de datos real.