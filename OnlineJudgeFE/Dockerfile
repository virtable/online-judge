FROM node:9.11.1-alpine
RUN apk add --no-cache git
WORKDIR /app
COPY OnlineJudgeFE/package*.json OnlineJudgeFE/
RUN cd OnlineJudgeFE && npm install
COPY . .
WORKDIR /app/OnlineJudgeFE
RUN npm run build:dll
RUN npm run build

