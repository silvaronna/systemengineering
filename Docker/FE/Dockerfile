# Gunakan image Node.js sebagai dasar
FROM node:20-slim AS builder

# Set working directory di dalam container
WORKDIR /app

# Salin file package.json dan package-lock.json terlebih dahulu
COPY package.json package-lock.json ./

# Install dependensi aplikasi pake fallback kalo ada konflik dependency
RUN npm install || (echo "⚠️  Warning: Konflik dependency terdeteksi, mencoba npm install --force" && npm install --force)

# Salin semua file aplikasi ke dalam container
COPY . .

# Build aplikasi Vite
RUN npm run build

# Gunakan image Nginx sebagai web server
FROM nginx:alpine

# Salin hasil build dari tahap sebelumnya ke direktori Nginx
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port 823
EXPOSE 823

# Jalankan Nginx
CMD ["nginx", "-g", "daemon off;"]