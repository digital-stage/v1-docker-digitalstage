FROM node:12.19.0-alpine AS build

ENV MONGO_URL=mongodb://mongo:27017
ENV AUTH_URL=http://digital-auth:5000
ENV PORT=4020

COPY package.json ./
COPY tsconfig.json ./
COPY ecosystem.config.js ./
RUN npm install
COPY src ./src
RUN npm run build

FROM node:12.19.0-alpine
ENV NODE_ENV=production
COPY package.json ./
RUN npm install
COPY --from=build /dist ./dist
EXPOSE 5000
ENTRYPOINT ["node", "./dist/index.js"]