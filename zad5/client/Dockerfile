FROM node:20-alpine3.20

WORKDIR /app

COPY package*.json ./

RUN npm install --legacy-peer-deps

COPY . .

RUN npm run build

CMD ["npm", "run", "start"]
