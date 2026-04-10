# Cluster Docker: Nginx Balanceador + Apache

Este proyecto arranca una infraestructura web con Docker Compose que incluye:
- **1 Contenedor Nginx** actuando como Proxy Inverso y Balanceador de Carga.
- **2 Contenedores Apache** (`httpd`) sirviendo contenido estático en el backend.
- **Caché de archivos** configurada en Nginx para mejorar el rendimiento.
- **Volumen Compartido** para que ambos backends de Apache sirvan exactamente la misma página web.

## 🚀 Requisitos Previos

- [Docker](https://www.docker.com/) instalado.
- [Docker Compose](https://docs.docker.com/compose/) instalado.

## 🛠️ Instalación y Uso

1. **Clonar el repositorio**:
   ```bash
   git clone https://github.com/paugapa/mi-cluster-docker.git
   cd mi-cluster-docker
   ```

2. **Añadir contenido multimedia (opcional)**:
   Por defecto, el archivo `index.html` requiere de imágenes y de un vídeo para renderizarse correctamente. Puedes crearlas dentro de la ruta `./html`:
   - Crea `html/images/` y añade `img1.jpg`, `img2.jpg` y `img3.jpg`.
   - Crea `html/videos/` y añade `sample.mp4`.

3. **Arrancar el Clúster**:
   Para levantar la infraestructura de forma desatendida, ejecuta:
   ```bash
   docker-compose up -d
   ```

4. **Acceso al Servicio**:
   Abre tu navegador web y visita: [http://localhost](http://localhost)

5. **Verificación del Balanceador de Carga y la Caché**:
   - Inspecciona las herramientas de desarrollador en tu navegador (`F12` -> pestaña Red/Network y revisa las peticiones).
   - Verás dos cabeceras personalizadas interesantes inyectadas por Nginx:
     - `X-Backend-Server`: Indica la IP del contenedor Apache que logró resolver la petición. Si fuerzas la recarga (Ctrl+F5) notarás cómo alterna entre los dos Apaches.
     - `X-Proxy-Cache`: Te mostrará un `HIT` si el archivo fue servido directamente desde la memoria de Nginx, o un `MISS` si lo tuvo que consultar a uno de los Apaches.

## 🛑 Detener el clúster

Para detener la infraestructura y la red de contenedores:
```bash
docker-compose down
```
