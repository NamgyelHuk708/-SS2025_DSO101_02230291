# builder phase
FROM node:14

WORKDIR '/app'

COPY package.json ./
RUN npm install --legacy-peer-deps

COPY ./ ./
RUN npm run build

FROM nginx
EXPOSE 80
CMD ["npm", "run", "start"]