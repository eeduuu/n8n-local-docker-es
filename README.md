# n8n-local-docker-es

Este repositorio incluye dos carpetas:

- `local-windows/` → para usar en **Windows** con Docker Desktop.
- `local-macos/` → para usar en **macOS** con Docker Desktop.

En ambos casos:

- Se levanta n8n con Docker.
- Se instala automáticamente el paquete **`cheerio`** para poder usarlo en los nodos de Código de n8n con:

~~~js
const cheerio = require('cheerio');
~~~

---

## 0. ¿Qué necesito antes de empezar?

> Nota: si alguno de los enlaces deja de funcionar en el futuro, basta con buscar
> “Docker Desktop Windows” o “Docker Desktop Mac” en tu buscador favorito.

### Requisitos en Windows

1. Instalar **Docker Desktop para Windows**.  
   Puedes descargarlo desde la página oficial de Docker:  
   [Docker Desktop](https://www.docker.com/products/docker-desktop/)

2. Durante la instalación, si Docker te pide activar **WSL2**, sigue los pasos que te muestre el asistente.

### Requisitos en macOS

1. Instalar **Docker Desktop para Mac**.  
   También se descarga desde la página oficial de Docker:  
   [Docker Desktop](https://www.docker.com/products/docker-desktop/)

2. Completa el asistente de instalación y asegúrate de que Docker Desktop se abre sin errores antes de seguir con los pasos del repositorio.

---

## 1. Descargar este repositorio

Tienes dos opciones: con Git o descargando el ZIP.

### Opción A – Usar Git

En una terminal (PowerShell en Windows o Terminal en macOS):

~~~bash
git clone https://github.com/TU-USUARIO/n8n-local-docker-es.git
~~~

Esto creará una carpeta llamada `n8n-local-docker-es`.

### Opción B – Descargar el ZIP

1. Entra en la página del repositorio en GitHub.
2. Haz clic en el botón verde **“Code”** → **“Download ZIP”**.
3. Descomprime el ZIP en una carpeta a tu elección.
4. Dentro verás algo como:

~~~text
n8n-local-docker-es/
├─ README.md
├─ local-windows/
└─ local-macos/
~~~

---

## 2. Cómo usarlo en Windows (paso a paso)

### 2.1. Abrir la carpeta `local-windows`

1. Abre el explorador de archivos.
2. Navega hasta la ruta donde clonaste o descomprimiste el repositorio.
3. Entra en la carpeta `n8n-local-docker-es`.
4. Dentro verás `local-windows`. Entra en esa carpeta.

Ejemplo de ruta:

~~~text
C:\Users\TUUSUARIO\Descargas\n8n-local-docker-es\local-windows
~~~

### 2.2. Abrir una terminal en esa carpeta

Forma sencilla:

1. Dentro de la carpeta `local-windows`, haz clic en un espacio en blanco.
2. Pulsa **Shift + clic derecho**.
3. Elige **“Abrir en Terminal de Windows”** o **“Abrir en PowerShell aquí”**.

La línea de la terminal debería terminar en algo así:

~~~text
C:\Users\TUUSUARIO\...\n8n-local-docker-es\local-windows>
~~~

Es importante que estés dentro de `local-windows`.

### 2.3. Parar contenedores antiguos (si los hubiera)

En esa terminal, escribe y pulsa **Enter**:

~~~bash
docker compose down
~~~

Si es la primera vez, es normal que diga que no hay contenedores.

### 2.4. Construir la imagen e iniciar n8n (instala cheerio)

En la misma terminal:

~~~bash
docker compose up -d --build
~~~

Este comando:

- Descarga la imagen oficial de n8n (si no la tienes).
- Construye una nueva imagen usando el `Dockerfile` (instala `cheerio`).
- Levanta el contenedor `n8n` en segundo plano.

La primera vez puede tardar unos minutos.

### 2.5. Comprobar que n8n está corriendo

Escribe:

~~~bash
docker ps
~~~

Deberías ver una línea con:

- `n8n` en la columna de nombre.
- `0.0.0.0:5678->5678` en la columna de puertos.

Si aparece, ¡n8n está arrancado!

### 2.6. Abrir n8n

Tienes dos formas de abrir n8n:

#### Opción A – Desde el navegador

Abre tu navegador (Chrome, Edge, etc.) y entra en:

~~~text
http://localhost:5678
~~~

Ahí ya puedes crear flujos, nodos, etc.

#### Opción B – Desde Docker Desktop

1. Abre **Docker Desktop**.
2. En la lista de contenedores, busca el contenedor llamado `n8n`.
3. Haz clic en el icono de abrir en navegador (suele ser un enlace/ botón tipo **“Open in browser”** o similar).
4. Se abrirá una pestaña del navegador apuntando a `http://localhost:5678`.

---

## 3. Cómo usarlo en macOS (paso a paso)

Los pasos son muy parecidos, solo cambia cómo abrir la Terminal y las rutas.

### 3.1. Abrir la carpeta `local-macos`

1. Abre **Finder**.
2. Ve a la carpeta donde clonaste o descomprimiste el repositorio.
3. Entra en `n8n-local-docker-es`.
4. Entra en `local-macos`.

Ejemplo de ruta:

~~~text
/Users/tuusuario/Downloads/n8n-local-docker-es/local-macos
~~~

### 3.2. Abrir la Terminal en esa carpeta

1. Abre la app **Terminal**.
2. Escribe `cd ` (cd + espacio, sin pulsar Enter aún).
3. Arrastra la carpeta `local-macos` desde Finder a la ventana de la Terminal.
4. Pulsa **Enter**.

Verás algo como:

~~~bash
cd /Users/tuusuario/Downloads/n8n-local-docker-es/local-macos
~~~

### 3.3. Parar contenedores antiguos

En esa Terminal:

~~~bash
docker compose down
~~~

### 3.4. Construir la imagen e iniciar n8n (con cheerio)

~~~bash
docker compose up -d --build
~~~

### 3.5. Comprobar que n8n está corriendo

~~~bash
docker ps
~~~

Deberías ver un contenedor `n8n` escuchando en el puerto 5678.

### 3.6. Abrir n8n

Tienes dos formas de abrir n8n:

#### Opción A – Desde el navegador

Abre tu navegador y entra en:

~~~text
http://localhost:5678
~~~

#### Opción B – Desde Docker Desktop

1. Abre **Docker Desktop** en tu Mac.
2. En la lista de contenedores, busca el contenedor llamado `n8n`.
3. Haz clic en el icono/enlace para **abrir en el navegador** (suele llamarse “Open in browser” o similar).
4. Se abrirá una pestaña del navegador apuntando a `http://localhost:5678`.

---

## 4. ¿Qué es cheerio y cómo usarlo en n8n?

**cheerio** es una librería de Node.js que permite leer y manipular HTML como si usaras jQuery, pero en el servidor.

En esta repo:

- El **Dockerfile** instala `cheerio` dentro de la imagen de n8n.
- El `docker-compose.yml` añade la variable `NODE_FUNCTION_ALLOW_EXTERNAL=cheerio` para que n8n permita usarlo en los nodos de Código.

### Ejemplo de uso en un nodo de Código de n8n

1. Crea un **Code node**.
2. Añade este código:

~~~js
const cheerio = require('cheerio');

// Supongamos que en $json.html viene HTML de una web
const $ = cheerio.load($json.html || '');

const title = $('title').text();

return [
  {
    json: {
      title,
    },
  },
];
~~~

Con eso puedes extraer elementos del HTML de forma sencilla.

---

## 5. Errores típicos y soluciones

### 5.1. `no configuration file provided: not found`

Este error aparece cuando ejecutas `docker compose` en una carpeta donde **no existe** `docker-compose.yml`.

✅ Solución:

- Asegúrate de estar en:
  - `local-windows` para Windows
  - `local-macos` para macOS

Antes de ejecutar:

~~~bash
docker compose up -d --build
~~~

Puedes comprobar los archivos de la carpeta con:

~~~bash
dir    # en Windows
ls     # en macOS
~~~

y ver que `docker-compose.yml` está ahí.

### 5.2. `Cannot find module 'cheerio'`

Significa que:

- La imagen de Docker no se construyó con `cheerio`, o
- Falta la variable `NODE_FUNCTION_ALLOW_EXTERNAL=cheerio`.

✅ Solución:

1. No modifiques el `Dockerfile` ni el `docker-compose.yml` que vienen en esta repo (al menos al principio).
2. Vuelve a construir e iniciar n8n:

~~~bash
docker compose down
docker compose up -d --build
~~~

Esto fuerza a Docker a reconstruir la imagen con `cheerio` y a levantar n8n con la configuración correcta.

---

## 6. Nota para el futuro

Si cambias de ordenador o montas n8n en otro PC:

1. Copia este repositorio (o vuelve a clonarlo).
2. Sigue los pasos de Windows o macOS.
3. Tus flujos de n8n podrán usar `cheerio` igual, usando siempre:

~~~js
const cheerio = require('cheerio');
~~~

---

## 7. Licencia

Este proyecto está licenciado bajo la licencia MIT.  
Consulta el archivo `LICENSE` para ver el texto completo.

Si este repositorio te resulta útil, puedes dejar una ⭐ en GitHub o abrir un issue con dudas o sugerencias.

---

## Autor

Creado por:

- 🌐 Web: [https://dupavi.es](https://dupavi.es)  
- 💼 LinkedIn: [Eduard Pampalona Viladot](https://www.linkedin.com/in/eeduuu-seo-ia/)

<p align="left">
  <a href="https://dupavi.es" target="_blank"><img src="https://img.shields.io/badge/DUPAVI.ES-f97316?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Web dupavi.es" /></a> &nbsp; <a href="https://www.linkedin.com/in/eeduuu-seo-ia/" target="_blank"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn - Eduard Pampalona Viladot" /></a>
</p>

