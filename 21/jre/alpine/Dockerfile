FROM eclipse-temurin:21-jre-alpine

RUN apk add -U --no-cache curl bash && apk upgrade --no-cache

ENV TZ=Pacific/Tahiti
ENV LANG=fr_FR:UTF-8
ENV LANGUAGE=fr
ENV LC_ALL=fr_FR.UTF-8

COPY 21/jre/alpine/install_certs-21 /tmp/install_certs
RUN bash -xe /tmp/install_certs
