# 🐳 Comandos Básicos de Docker

Referencia rápida de los comandos más importantes de Docker, organizados por categoría. Ideal para quienes están aprendiendo o necesitan un recordatorio en el día a día.

---

## 📋 Tabla de contenidos

- [Imágenes](#-imágenes)
- [Contenedores](#-contenedores)
- [Volúmenes](#-volúmenes)
- [Redes](#-redes)
- [Sistema](#-sistema)

---

## 📦 Imágenes

| Comando | Descripción |
|--------|-------------|
| `docker pull <imagen>` | Descarga una imagen desde Docker Hub |
| `docker images` | Lista todas las imágenes locales |
| `docker build -t <nombre> .` | Construye una imagen desde un `Dockerfile` |
| `docker rmi <imagen>` | Elimina una imagen local |

### Ejemplos

```bash
# Descargar una imagen específica
docker pull ubuntu:22.04

# Construir con nombre y etiqueta
docker build -t mi-app:1.0 .

# Listar imágenes (incluyendo intermedias)
docker images -a

# Eliminar una imagen
docker rmi nginx
```

---

## 🛳️ Contenedores

| Comando | Descripción |
|--------|-------------|
| `docker run <imagen>` | Crea y ejecuta un nuevo contenedor |
| `docker ps` | Lista los contenedores en ejecución |
| `docker ps -a` | Lista todos los contenedores (incluye detenidos) |
| `docker stop <contenedor>` | Detiene un contenedor (señal SIGTERM) |
| `docker start <contenedor>` | Inicia un contenedor detenido |
| `docker restart <contenedor>` | Reinicia un contenedor |
| `docker rm <contenedor>` | Elimina un contenedor detenido |
| `docker exec -it <contenedor> bash` | Abre una terminal dentro del contenedor |
| `docker logs <contenedor>` | Muestra los logs del contenedor |
| `docker inspect <contenedor>` | Muestra detalles en formato JSON |

### Flags más usados con `docker run`

| Flag | Descripción |
|------|-------------|
| `-d` | Ejecuta en segundo plano (detached) |
| `-p 8080:80` | Mapea puerto del host al contenedor |
| `--name mi-app` | Asigna un nombre al contenedor |
| `-it` | Modo interactivo con terminal |
| `--rm` | Elimina el contenedor al detenerlo |
| `-e VAR=valor` | Define una variable de entorno |
| `-v ruta:ruta` | Monta un volumen |

### Ejemplos

```bash
# Correr nginx en segundo plano, expuesto en el puerto 8080
docker run -d -p 8080:80 --name mi-nginx nginx

# Abrir una terminal interactiva en Ubuntu
docker run -it ubuntu:22.04 bash

# Ver logs en tiempo real (últimas 50 líneas)
docker logs -f --tail 50 mi-nginx

# Entrar a un contenedor ya en ejecución
docker exec -it mi-nginx bash

# Eliminar todos los contenedores detenidos
docker rm $(docker ps -aq)
```

---

## 💾 Volúmenes

Los volúmenes permiten que los datos persistan aunque el contenedor sea eliminado.

| Comando | Descripción |
|--------|-------------|
| `docker volume create <nombre>` | Crea un nuevo volumen |
| `docker volume ls` | Lista todos los volúmenes |
| `docker volume rm <nombre>` | Elimina un volumen |
| `docker volume prune` | Elimina todos los volúmenes sin uso |

### Ejemplos

```bash
# Crear un volumen
docker volume create mis-datos

# Usar un volumen al correr un contenedor
docker run -d -v mis-datos:/app/data mi-app

# Montar una carpeta local (bind mount)
docker run -d -v $(pwd)/data:/app/data mi-app
```

---

## 🌐 Redes

Las redes permiten que los contenedores se comuniquen entre sí por nombre.

| Comando | Descripción |
|--------|-------------|
| `docker network create <nombre>` | Crea una red virtual |
| `docker network ls` | Lista todas las redes disponibles |
| `docker network rm <nombre>` | Elimina una red |
| `docker network inspect <nombre>` | Muestra detalles de la red |

### Ejemplos

```bash
# Crear una red personalizada
docker network create mi-red

# Conectar dos contenedores a la misma red
docker run -d --network mi-red --name db postgres
docker run -d --network mi-red --name app mi-app

# Desde "app", puedes acceder a "db" por su nombre
```

---

## ⚙️ Sistema

| Comando | Descripción |
|--------|-------------|
| `docker version` | Muestra la versión del cliente y del daemon |
| `docker info` | Información general del sistema Docker |
| `docker stats` | Monitorea CPU, memoria y red en tiempo real |
| `docker system prune` | Elimina todos los recursos sin uso |
| `docker system prune -a --volumes` | Limpieza total (imágenes, contenedores, volúmenes) |

### Ejemplos

```bash
# Ver consumo de recursos en tiempo real
docker stats

# Limpiar espacio (contenedores detenidos, imágenes sin tag, redes)
docker system prune

# Limpieza profunda (¡cuidado, borra todo lo que no esté en uso!)
docker system prune -a --volumes
```

---

## 🧩 Referencia rápida

```
docker pull      → descargar imagen
docker build     → construir imagen
docker run       → crear y ejecutar contenedor
docker ps        → listar contenedores
docker stop      → detener contenedor
docker rm        → eliminar contenedor
docker exec      → ejecutar comando dentro del contenedor
docker logs      → ver logs
docker volume    → gestionar volúmenes
docker network   → gestionar redes
docker system    → administración del sistema
```

---

## 📚 Recursos útiles

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Play with Docker (entorno online)](https://labs.play-with-docker.com/)

---

> 💡 **Tip:** Usa `docker <comando> --help` para ver todas las opciones disponibles de cualquier comando.
