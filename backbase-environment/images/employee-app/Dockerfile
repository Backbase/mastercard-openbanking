FROM node:16 AS builder

RUN curl -s "https://start.backbase.com/productised/product-employee-web?version=2023.02-LTS" -o employee-app-package.zip
RUN unzip employee-app-package.zip -d /tmp/employee-app-package

WORKDIR /tmp/employee-app-package/web/employee-app

RUN --mount=type=secret,id=npm,dst=./.npmrc npm i --legacy-peer-deps
RUN npm run build:employee-app

FROM repo.backbase.com/backbase-docker-releases/web-base:1.1.4

COPY --from=builder /tmp/employee-app-package/web/employee-app/dist/employee-app /statics
