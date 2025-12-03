# Ejercicio 1: Dockerfile

## ¿Qué es un Dockerfile?
Un Dockerfile es un archivo de texto que contiene instrucciones para construir una imagen Docker. Permite definir:
- Imagen base
- Dependencias
- Archivos a copiar
- Comando a ejecutar

## Nuestro Dockerfile
Explicación de cada sección:

- `FROM node:18-alpine`: usa Node.js 18 en Alpine (ligero)
- `LABEL maintainer="tu-email"`: metadatos de la imagen
- `WORKDIR /app`: directorio de trabajo dentro del contenedor
- `COPY package*.json ./`: copia solo dependencias para aprovechar caché
- `RUN npm ci --only=production`: instala dependencias
- `COPY index.js test.js ./`: copia el código
- `EXPOSE 3000`: documenta puerto usado
- `USER nodejs`: ejecuta con usuario no-root
- `CMD ["node", "index.js"]`: comando por defecto

## Construir y ejecutar localmente
```bash
docker build -t cicd-demo:latest .
docker images
docker run --rm cicd-demo:latest
docker logs <container-id>
