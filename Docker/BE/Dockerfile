# Menggunakan Node.js versi 20 sebagai base image
FROM node:20

# Set working directory
WORKDIR /app

# Copy package.json dan package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install
# Install nano untuk editor dan dotenv untuk env handling
RUN apt-get update && apt-get install -y nano
RUN apt-get update && apt-get install -y dotenv

# Copy folder prisma dan generate Prisma Client
COPY prisma ./prisma
RUN npx prisma generate

# Copy seluruh kode aplikasi ke dalam image
COPY . .

# Menjalankan backend
CMD ["node", "index.js"]