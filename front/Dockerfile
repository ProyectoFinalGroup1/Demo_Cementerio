# Usa una imagen de Node.js
FROM node:18 AS builder

# Establece el directorio de trabajo
WORKDIR /app

# Copia los archivos y las dependencias
COPY package*.json ./
RUN npm install

# Copia el resto del código
COPY . .

# Construye la aplicación
RUN npm run build

# Segunda etapa: Servidor optimizado
FROM node:18 AS runner

WORKDIR /app

# Copia solo el build generado
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./

# Expone el puerto 3000 (o el que uses)
EXPOSE 3000

# Comando para ejecutar Next.js en producción
CMD ["npm", "run", "start"]