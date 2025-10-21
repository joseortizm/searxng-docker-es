# Instalar y ejecutar SearXNG en macOS con Docker

> ⚙️ Esta guía te permite ejecutar **SearXNG** de forma local en tu Mac usando Docker.  
> Ideal para pruebas, desarrollo o integración como API en tu proyecto.

## ¿Qué incluye?

| Name                                          | Description                                                    | Docker image                                                                 | Dockerfile                                                                                                                                                                                    |
|-----------------------------------------------|----------------------------------------------------------------|------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SearXNG](https://github.com/searxng/searxng) | SearXNG by itself                                              | [docker.io/searxng/searxng:latest](https://hub.docker.com/r/searxng/searxng) | [builder.dockerfile](https://github.com/searxng/searxng/blob/master/container/builder.dockerfile) [dist.dockerfile](https://github.com/searxng/searxng/blob/master/container/dist.dockerfile) |
| [Valkey](https://github.com/valkey-io/valkey) | In-memory database                                             | [docker.io/valkey/valkey:8-alpine](https://hub.docker.com/r/valkey/valkey)   | [Dockerfile](https://github.com/valkey-io/valkey-container/blob/mainline/Dockerfile.template)                                                                                                 |

## 📋 Requisitos previos

Antes de comenzar, asegúrate de tener instalado:

- **Docker Desktop** para macOS  
  👉 [Descargar desde Docker](https://docs.docker.com/install/)

---

## ¿Cómo usarlo?

1. Clonar searxng-docker-es

```shell
git clone https://github.com/joseortizm/searxng-docker-es.git
cd searxng-docker-es
```

2. Verificar si el puerto 8080 está libre

SearXNG utiliza el puerto `8080` de tu computadora. Antes de iniciarlo, comprueba que no esté ocupado:
```shell
lsof -i :8080
```

3. Generar una clave secreta aleatoria (solo una vez)

SearXNG necesita una clave privada para encriptar sesiones y cookies. 
Ejecuta este comando en la terminal (desde la carpeta raíz del proyecto):
```shell
`sed -i '' "s|ultrasecretkey|$(openssl rand -hex 32)|g" searxng/settings.yml`
```
Esto reemplazará automáticamente el texto ```ultrasecretkey``` 
por una clave aleatoria dentro del archivo ```searxng/settings.yml```.

### Estos pasos son repetitivos luego de la configuración previa

4. Iniciar Docker Desktop

Abre Docker Desktop y déjalo ejecutándose (no necesitas hacer nada más allí).
Asegúrate de que el ícono de Docker esté activo en la barra superior de tu Mac.

5. Iniciar SearXNG

En la terminal, estando dentro del la carpeta raíz del repositorio ```searxng-docker-es```:
```shell
docker compose up
```

6. Abrir SearXNG en el navegador

Abre tu navegador y visita:
```shell
http://localhost:8080/
```

7. Probar la API (modo JSON)

Si deseas usarlo como API (por ejemplo, para integrarlo con tu LMS),
puedes obtener resultados en formato JSON:
```shell
http://localhost:8080/search?q=python&format=json
```

8. Detener la ejecución

Para detener SearXNG, presiona:
```shell
Ctrl + C
```

9. Verificar si sigue corriendo

Puedes comprobar si los contenedores continúan activos con:
```shell
docker ps
```
