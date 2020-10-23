FROM node:12.19.0-alpine AS build
ENV USE_SSL=false
ENV MONGO_URL=mongodb://mongo:27017

RUN apk add git && git clone https://github.com/digital-stage/auth-server.git \
 && cd auth-server \
 && npm install \
 && npm run build

FROM node:12.19.0-alpine
ENV NODE_ENV=production
COPY --from=build /auth-server/package.json ./
RUN npm install
COPY --from=build /auth-server/dist ./dist
EXPOSE 5000
ENTRYPOINT ["node", "./dist/index.js"]