FROM node:12.19.0-alpine AS build
ENV NEXT_PUBLIC_USE_SSL=false
ENV PORT=3000

COPY . ./
RUN rm .env* && npm install && npm run build
EXPOSE 3000
#ENTRYPOINT ["npm", "run", "start"]
ENTRYPOINT ["npm", "run", "dev"]