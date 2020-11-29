FROM node:14.15.0-buster AS build

ENV MONGO_DB=digitalstage
ENV MONGO_COLLECTION=routers
ENV AUTH_URL=http://digital-auth:5000
ENV PORT=4020

RUN git clone https://github.com/digital-stage/router-distributor.git \
 && cd router-distributor \
 && npm install \
 && npm run build

FROM node:14.15.0-buster
ENV NODE_ENV=production
COPY --from=build /router-distributor/package.json ./
RUN npm install
COPY --from=build /router-distributor/dist ./dist
EXPOSE 5000
ENTRYPOINT ["node", "./dist/index.js"]