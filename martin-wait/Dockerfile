# Filename: Dockerfile
FROM alpine:3.7

RUN apk add --no-cache netcat-openbsd

ADD wait /wait

ENTRYPOINT ["/wait"]
