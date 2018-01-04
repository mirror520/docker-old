FROM node:6-alpine

RUN npm install -g yarn
RUN npm install -g @angular/cli

RUN mkdir /app
WORKDIR /app

EXPOSE 4200

CMD ng serve --host 0.0.0.0 --public-host mis.secretariat.taichung.gov.tw:4200
