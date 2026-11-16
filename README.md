# Instalación y ejemplo inicial sin controlador

# Instalación de Node.js, NVM y NPM

# Índice

1. [Instalación y ejemplo inicial sin controlador](#instalación-y-ejemplo-inicial-sin-controlador)
   1. [Instalación de Node.js, NVM y NPM](#instalación-de-nodejs-nvm-y-npm)
      1. [¿Qué son?](#1-qué-son)
      2. [Instalación de NVM](#2-instalación-de-nvm)
         - [En Linux / macOS](#en-linux--macos)
         - [En Windows](#en-windows)
      3. [Instalar Node.js con NVM](#3-instalar-nodejs-con-nvm)
      4. [NPM (Node Package Manager)](#4-npm-node-package-manager)
      5. [Verificación final](#5-verificación-final)
2. [Creación inicial de un proyecto Node.js con Módulos (type: "module")](#creación-inicial-de-un-proyecto-nodejs-con-módulos-type-module)
   1. [Crear carpeta y proyecto](#1-crear-carpeta-y-proyecto)
   2. [Configurar Node para usar módulos ES](#2-configurar-node-para-usar-módulos-es)
   3. [Estructura básica del proyecto](#3-estructura-básica-del-proyecto)
      - [Comparativa CommonJS vs ES Modules](#comparativa-commonjs-vs-es-modules)
   4. [Código de prueba con librerías decorativas](#4-código-de-prueba-con-librerías-decorativas)
   5. [Instalación de Nodemon](#5-instalación-de-nodemon)
3. [Express.js (Servidor básico con rutas y JSON)](#expressjs-servidor-básico-con-rutas-y-json)
   1. [¿Qué es Express?](#1-qué-es-express)
   2. [Instalación inicial](#2-instalación-inicial)
   3. [Código completo y comentado](#3-código-completo-y-comentado)
      - [database.js](#databasejs)
   4. [Explicación general](#4-explicación-general)
   5. [Métodos HTTP usados](#5-métodos-http-usados)
   6. [Próximos pasos](#6-próximos-pasos)



## 1. ¿Qué son?

| Herramienta | Descripción |
| --- | --- |
| **Node.js** | Entorno que permite ejecutar JavaScript fuera del navegador (por ejemplo, en servidores o terminal). |
| **NPM** (Node Package Manager) | Gestor de paquetes de Node.js. Se instala automáticamente junto con Node. |
| **NVM** (Node Version Manager) | Permite instalar y cambiar fácilmente entre diferentes versiones de Node.js. |

## ⚙️ 2. Instalación de **NVM**

🪄 Recomendado: instala Node usando **NVM**, así puedes tener varias versiones sin conflictos.

### 🔹 En **Linux / macOS**

1. Abre la terminal y ejecuta:

```kotlin
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```

o con **wget**:

```kotlin
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```

1. Cierra y vuelve a abrir la terminal (o ejecuta):

```kotlin
source ~/.bashrc
# o en macOS:
source ~/.zshrc
```

1. Comprueba que se instaló:

```kotlin
nvm --version
```

---

### 🔹 En **Windows**

Usa **nvm-windows**, una versión adaptada:

1. Descarga el instalador desde
    
    👉 [https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)
    

```kotlin
nvm version
```

## 🟢 3. Instalar Node.js con NVM

Una vez tengas NVM:

```kotlin
nvm install --lts       # Instala la versión LTS (estable)
nvm install 22.11.0     # Instala una versión específica (ejemplo)
nvm use 22.11.0         # Cambia a esa versión
nvm list                # Muestra las versiones instaladas
```

✅ Para usar siempre una versión por defecto:

```kotlin
nvm alias default 22.11.0
```

---

## 📦 4. NPM (Node Package Manager)

NPM **viene incluido** con Node.js.

Comprueba que esté instalado:

```kotlin
npm -v
```

🧩 Comandos básicos de NPM:

| Comando | Descripción |
| --- | --- |
| `npm init` | Crea un nuevo proyecto Node (package.json). |
| `npm install paquete` | Instala un paquete local. |
| `npm install -g paquete` | Instala un paquete global. |
| `npm uninstall paquete` | Desinstala un paquete. |
| `npm update` | Actualiza dependencias. |
| `npm list` | Muestra paquetes instalados. |

## 🧩 5. Verificación final

```kotlin
node -v   # versión de Node
npm -v    # versión de npm
nvm list  # versiones disponibles
```

---

---

---

# Creación inicial de un proyecto Node.js con Módulos (`type: "module"`)

## 📦 1. Crear carpeta y proyecto

```kotlin
mkdir mi-proyecto
cd mi-proyecto
npm init -y
```

📝 Esto crea un archivo **`package.json`** básico con configuración predeterminada.

---

## ⚙️ 2. Configurar Node para usar **módulos ES (ECMAScript Modules)**

Por defecto, Node usa **CommonJS** (`require` y `module.exports`).

Para usar la sintaxis moderna **ESM** (`import` / `export`), edita tu `package.json` y agrega:

```kotlin
{
  "name": "mi-proyecto",
  "version": "1.0.0",
  "type": "module",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  },
  "devDependencies": {
    "nodemon": "^3.1.14"
  }
}
```

🔹 La clave `"type": "module"` le indica a Node que el proyecto usa sintaxis moderna de import/export.

📝 Nota: `nodemon` se declara en `devDependencies` porque solo se usa en desarrollo, nunca en producción. El script `dev` permite arrancar el servidor con recarga automática ejecutando `npm run dev`.
****

## **📁 3. Estructura básica del proyecto**

```kotlin
mi-proyecto/
├── package.json
├── app.js

```

⚖️ Comparativa: CommonJS vs ECMAScript Modules

| Característica | 🧱 **CommonJS (CJS)** | 🌐 **ES Modules (ESM)** |
| --- | --- | --- |
| **Activación** | Por defecto en Node.js | Requiere `"type": "module"` en `package.json` o extensión `.mjs` |
| **Sintaxis de importación** | `const x = require('x')` | `import x from 'x'` |
| **Sintaxis de exportación** | `module.exports = ...` o `exports.nombre = ...` | `export default ...` o `export const nombre = ...` |
| **Extensión de archivos** | `.js` (por defecto) | `.js` o `.mjs` (si no se define `"type": "module"`) |
| **Carga de módulos** | Síncrona (bloqueante) | Asíncrona (no bloqueante) |
| **Scope (ámbito)** | Cada archivo tiene su propio scope | Igual, pero con *strict mode* activado por defecto |
| **Compatibilidad con navegador** | ❌ No (solo Node) | ✅ Sí (misma sintaxis que en el navegador) |
| **Importación dinámica** | Con `require()` directamente | Con `import()` (devuelve una Promesa) |
| **Uso de `__dirname` y `__filename`** | Disponible automáticamente | No existen (hay que construirlos con `import.meta.url`) |
| **Ecosistema histórico** | La mayoría de los paquetes antiguos de Node están en CJS | Los paquetes modernos y frontend usan ESM |
| **Exportaciones múltiples** | Se exporta un objeto (`module.exports = {}`) | Se pueden exportar valores individuales o por defecto |
| **Performance** | Más rápido en carga por ser síncrono (para módulos locales) | Más flexible, ideal para módulos asíncronos o compartidos con frontend |

## **📁 4. Estructura básica del proyecto**

El código para probar que funciona (con librerías decorativas)

```kotlin
npm i chalk
o
npm i kleur
```

Código de ejemplo:

```jsx
import chalk from 'chalk'
import kleur from 'kleur';

console.log(kleur.green().bold('🟢 Éxito'));
console.log(chalk.blue('✅ Texto verde'));
```

Para ejecutarlo:

```jsx
node app
```

## **📁 5. Instalación de Nodemon**

Para evitar tener que levantar el servidor con cada cambio podemos instalar el paquete nodemon:

```jsx
npm i nodemon
```

Levantamos el servidor con:

```jsx
nodemon
```

En la terminal, tendremo:

```jsx
usuario@Mac Ejemplo_borrar % nodemon
[nodemon] 3.1.9
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,cjs,json
[nodemon] starting `node app.js`
🟢 Éxito
✅ Texto verde
[nodemon] clean exit - waiting for changes before restart
```

---

---

---

# Express.js (Servidor básico con rutas y JSON)

## 🚀 1. ¿Qué es Express?

**Express.js** es una **librería minimalista** para Node.js que facilita la creación de servidores web y APIs REST. Permite definir **rutas HTTP**, manejar **peticiones y respuestas** fácilmente y trabajar con **middlewares**.

- Es **una librería minimalista** para Node.js.
- Te proporciona herramientas para:
    - Crear servidores HTTP.
    - Definir rutas.
    - Manejar middlewares y peticiones/respuestas.
- Pero **no impone una estructura de proyecto**, ni controla todo el flujo de tu aplicación.

💡 Por eso, aunque se habla de “framework” por simplicidad, **lo correcto es llamarlo librería de servidor para Node.js**.

---

## ⚙️ 2. Instalación inicial

1. Crear el proyecto (si aún no lo tienes):

```bash
mkdir mi-api
cd mi-api
npm init -y
```

1. Instalar dependencias:

```bash
npm install express chalk kleur nodemon
```

- **express** → framework para el servidor.
- **chalk / kleur** → librerías para mostrar mensajes coloridos en consola. Kleur es un poco más ligero.

⚠️ Desde la versión 6, **Chalk es ESM-only** (ya no soporta `require`). Al usar `"type": "module"` en nuestro `package.json` no hay problema, pero si alguna vez trabajas en un proyecto CommonJS deberás fijar Chalk en una versión `^4` o `^5` (las últimas compatibles con CJS).

## **🧩 3. Código completo y comentado**

```jsx
// Importamos las librerías necesarias
import express from 'express'
import chalk from 'chalk'
import kleur from 'kleur'

// Importamos las funciones del "módulo de base de datos" (archivo local)
import { addValue,
    addValueAt,
    getValue,
    getValues,
    removeValueAt,
    updateValueAt } from './database/database.js'

// Creamos la app de Express
const app = express()

// Definimos el puerto del servidor
const port = 9090

// Middleware que permite recibir y procesar JSON en las peticiones
app.use(express.json())

// --------------------------------------------
// RUTAS (Endpoints de la API)
// --------------------------------------------

// GET / → Devuelve todo el vector y un mensaje
app.get('/', (req,res) => {
    res.status(200).json({
        'msg' : 'Gestión del vector',
        'valores' : getValues()
    })
})

// GET /:id → Devuelve el valor en una posición concreta
app.get('/:id', (req,res) => {
    let indice = parseInt(req.params.id, 10)
    res.status(200).json({
        'pos' : indice,
        'valor' : getValue(indice)
    })
})

// DELETE /:id → Elimina un elemento según su posición
app.delete('/:id', (req, res) => {
    let indice = parseInt(req.params.id,10)
    removeValueAt(indice)
    res.status(200).json({
        'msg' : 'Elemento borrado',
        'valores' : getValues()
    })
})

// POST / → Inserta un nuevo valor al final del vector
app.post('/',(req, res) => {
    let nuevoValor = req.body.valor
    addValue(nuevoValor)
    res.status(200).json({
        'msg' : 'Elemento insertado',
        'valores' : getValues()
    })
})

// POST /:id → Inserta un valor en una posición concreta
app.post('/:id',(req, res) => {
    let pos = req.params.id
    let nuevoValor = req.body.valor
    addValueAt(nuevoValor, pos)
    res.status(200).json({
        'msg' : 'Elemento insertado',
        'valores' : getValues()
    })
})

// PUT /:id → Actualiza un valor existente
app.put('/:id',  (req, res) => {
    let indice = parseInt(req.params.id,10)
    updateValueAt(indice, req.body.valor)
    res.status(200).json({
        'msg' : 'Elemento modificado',
        'valores' : getValues()
    })
})

// --------------------------------------------
// SERVIDOR EN ESCUCHA
// --------------------------------------------

// Inicia el servidor y muestra mensaje en consola
app.listen(port, () => {
  console.log(chalk.green(`✅ Servidor corriendo en ${port}`))
})
```

Siendo la base de datos, database.js:

```jsx
let valores = [1,2,3,4,5]

export const addValue = (valor) => {
    valores.push(valor);
}

export const addValueAt = (nuevoValor,i) => {
    valores.splice(i, 0, nuevoValor);
}

export const getValues = () => {
    return valores;
}

export const getValue = (i) => {
    return valores[i];
}

export const removeValueAt = (i) => {
    valores.splice(i, 1);
}

export const updateValueAt = (i, p) => {
    valores[i] = p;
}

export const size = () => {
    return valores.length
}

// export {
//     getValores,
//     getValorAt,
//     size
// }
```

## 🧠 4. Explicación general

| Elemento | Función |
| --- | --- |
| `app.use(express.json())` | Middleware que convierte automáticamente el cuerpo de las peticiones a JSON. |
| `req.params` | Accede a parámetros enviados en la URL (`/usuarios/:id`). |
| `req.body` | Accede al contenido del cuerpo de la petición (solo si se usa `express.json()`). |
| `res.status().json()` | Envía una respuesta con código HTTP y datos JSON. |
| `app.listen(port)` | Inicia el servidor para escuchar peticiones en un puerto concreto. |

⚠️ **Cuidado con el orden de las rutas:** Express evalúa las rutas en el orden en que se declaran. Como `/:id` es una ruta dinámica que acepta *cualquier* valor (texto o número), una petición como `GET /foo` también entrará por esa ruta, devolviendo `valor: undefined` en vez de un error 404. Para un ejemplo real conviene validar que `id` sea numérico (o usar `express-validator`) antes de usarlo como índice del vector.

Además, nótese que `req.params.id` siempre llega como **string**. Por eso en `GET /:id`, `PUT /:id` y `DELETE /:id` convertimos el valor con `parseInt(req.params.id, 10)` antes de usarlo como índice; si se te olvida, `array[String]` puede dar resultados inesperados (aunque JS suele convertir el índice implícitamente, es una mala práctica dejarlo así).

## 📡 5. Métodos HTTP usados

| Método | Propósito | Ejemplo |
| --- | --- | --- |
| `GET` | Consultar datos | `/` o `/:id`  o `/:id?` |
| `POST` | Crear o insertar nuevos datos | `/` o `/:id` o `/:id?` |
| `PUT` | Actualizar datos existentes | `/:id` |
| `DELETE` | Eliminar datos | `/:id` |

---

## 🧩 6. Próximos pasos (para completar el proyecto)

🔜 Puedes mejorar este código añadiendo:

- **Controladores** → separar la lógica de cada ruta.
- **Validaciones** de entrada (`express-validator`).
- **Manejo de errores global** con `app.use((err, req, res, next) => { ... })`.
- **CORS y seguridad** (`cors`, `jwt`).