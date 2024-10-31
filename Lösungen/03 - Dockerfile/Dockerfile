# Um diese **node** app zu bauen muss dieser Befehl ausgeführt werden: yarn install --production
# Erstellen sie ein Dockerfile welches die App baue und unter dem Port 3000 exposed

FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000