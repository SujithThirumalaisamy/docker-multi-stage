FROM node:20-slim AS installer

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

FROM node:20-alpine AS builder

WORKDIR /app

COPY --from=installer /app/node_modules ./node_modules

COPY . .

RUN npm run build

FROM node:20-alpine AS runner

WORKDIR /app

COPY --from=builder /app/dist ./

EXPOSE 3000

CMD ["node", "index.js"]
