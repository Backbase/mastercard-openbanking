FROM node:16 AS builder

RUN --mount=type=secret,id=repo,dst=./.netrc curl --netrc-file .netrc -s "https://repo.backbase.com/artifactory/backbase-releases/com/backbase/apps/employee-app/employee-essentials-2023.09.3-LTS.zip" -o employee-essentials-package.zip
RUN unzip employee-essentials-package.zip -d /tmp/employee-essentials-package

WORKDIR /tmp/employee-essentials-package

RUN npm i -g nx
RUN --mount=type=secret,id=npm,dst=./.npmrc npm ci --ignore-scripts --legacy-peer-deps
RUN nx build employee-essentials

FROM repo.backbase.com/backbase-docker-releases/web-base:2.0.8

COPY --from=builder /tmp/employee-essentials-package/dist/apps/employee-essentials /statics
