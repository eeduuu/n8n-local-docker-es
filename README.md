# n8n-local-docker-es

Este repositorio contiene ejemplos mínimos para levantar **n8n local con Docker** en:

- Windows (`local-windows/`)
- macOS (`local-macos/`)

En ambos casos se incluye la instalación de **cheerio** como extra para poder usarlo en los nodos de Código de n8n mediante:

```js
const cheerio = require('cheerio');
```

---

## Cómo usar (Windows)

1. Instala Docker Desktop.
2. Descarga este repositorio (o el ZIP) y descomprímelo.
3. Abre una terminal en la carpeta `local-windows` del repositorio.

   Ejemplo:
   ```bash
   cd ruta/del/repositorio/n8n-local-docker-es/local-windows
   ```

4. Para asegurarte de que no hay contenedores antiguos:

   ```bash
   docker compose down
   ```

5. Construye la imagen (instala cheerio) y levanta n8n:

   ```bash
   docker compose up -d --build
   ```

6. Comprueba que n8n está corriendo:

   ```bash
   docker ps
   ```

   Deberías ver un contenedor llamado `n8n` en el puerto `5678`.

7. Abre n8n en el navegador:

   ```text
   http://localhost:5678
   ```

---

## Cómo usar (macOS)

1. Instala Docker Desktop.
2. Descarga este repositorio (o el ZIP) y descomprímelo.
3. Abre la Terminal en la carpeta `local-macos` del repositorio, por ejemplo:

   ```bash
   cd /ruta/al/repositorio/n8n-local-docker-es/local-macos
   ```

4. Para parar contenedores antiguos:

   ```bash
   docker compose down
   ```

5. Construye la imagen e inicia n8n (con cheerio instalado):

   ```bash
   docker compose up -d --build
   ```

6. Comprueba:

   ```bash
   docker ps
   ```

7. Abre n8n en el navegador:

   ```text
   http://localhost:5678
   ```

---

## Uso de cheerio dentro de n8n

Gracias a la configuración del `Dockerfile` (instala cheerio) y la variable
`NODE_FUNCTION_ALLOW_EXTERNAL=cheerio` en `docker-compose.yml`, puedes usar
cheerio en un nodo de Código de n8n así:

```js
const cheerio = require('cheerio');

const $ = cheerio.load($json.html || '');
const title = $('title').text();

return [
  {
    json: {
      title,
    },
  },
];
```

---

## Errores típicos

- `no configuration file provided: not found`  
  Ejecutaste `docker compose` fuera de la carpeta que contiene `docker-compose.yml`.
  Solución: sitúate en `local-windows` o `local-macos` antes de ejecutar los comandos.

- `Cannot find module 'cheerio'`  
  O bien la imagen no se construyó con cheerio, o falta
  `NODE_FUNCTION_ALLOW_EXTERNAL=cheerio`. Vuelve a revisar el `Dockerfile` y el
  `docker-compose.yml` y ejecuta:

  ```bash
  docker compose down
  docker compose up -d --build
  ```
