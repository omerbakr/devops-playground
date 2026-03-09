FROM node:22-alpine AS base

WORKDIR /app

COPY package*.json package-lock.json* ./

RUN npm ci --omit=dev

COPY . .

# Run as non-root user (alpine node image has a non-root user named 'node')
USER node

EXPOSE 3000

ENV NODE_ENV=production

CMD ["npm", "start"]