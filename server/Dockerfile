FROM node:14.15.0-buster AS build
ENV PORT=4000
ENV USE_SSL=false
ENV USE_REDIS=false
ENV MONGO_URL=mongodb://mongo:27017
ENV AUTH_URL=http://digital-auth:5000

RUN git clone https://github.com/digital-stage/server.git \
    && cd server \
    && npm install \
    && npm run build

FROM node:14.15.0-buster
ENV NODE_ENV=production
COPY --from=build /server/package.json ./
RUN npm install
COPY --from=build /server/dist ./dist
EXPOSE 4000
ENTRYPOINT ["node", "./dist/index.js"]