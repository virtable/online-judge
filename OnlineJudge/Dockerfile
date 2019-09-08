FROM node:9.11.1-alpine as build
RUN apk add --no-cache git
WORKDIR /app
COPY OnlineJudgeFE/package*.json OnlineJudgeFE/
RUN cd OnlineJudgeFE && npm install
COPY . .
WORKDIR /app/OnlineJudgeFE
RUN npm run build:dll
RUN npm run build

FROM python:3.7-alpine3.9

ENV OJ_ENV production

ADD OnlineJudge /app
WORKDIR /app

HEALTHCHECK --interval=5s --retries=3 CMD python2 /app/deploy/health_check.py

RUN apk add --update --no-cache build-base nginx openssl curl unzip supervisor jpeg-dev zlib-dev postgresql-dev freetype-dev && \
    pip install --no-cache-dir -r /app/deploy/requirements.txt && \
    apk del build-base --purge

COPY --from=build /app/OnlineJudgeFE/dist dist

ENTRYPOINT /app/deploy/entrypoint.sh
