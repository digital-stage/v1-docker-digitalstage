FROM node:12.19.0-alpine AS build

ENV MONGO_URL=mongodb://mongo:27017
ENV AUTH_URL=http://digital-auth:5000
ENV PORT=4020

RUN apk add git && git clone https://github.com/digital-stage/router-distributor.git \
 && cd router-distributor \
 && npm install \
 && npm run build

FROM node:12.19.0-alpine
ENV NODE_ENV=production
COPY --from=build /router-distributor/package.json ./
RUN npm install
COPY --from=build /router-distributor/dist ./dist
EXPOSE 5000
ENTRYPOINT ["node", "./dist/index.js"]