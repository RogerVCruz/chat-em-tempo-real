# Stage 1 - Montar a base
FROM node:18-alpine AS base
WORKDIR /app
COPY src ./src
COPY package*.json ./
COPY tsconfig*.json ./
RUN npm install

# Stage 2 - Montar a aplicação
FROM base AS build
WORKDIR /app
RUN npm run build

# Stage 3 - Produção
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --only-production
COPY --from=build /app/build ./

CMD ["node", "main.js"]