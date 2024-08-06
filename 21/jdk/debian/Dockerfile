FROM eclipse-temurin:21

RUN apt-get update && apt-get install -y --no-install-recommends locales curl \
    && sed -i -e 's/# fr_FR.UTF-8 UTF-8/fr_FR.UTF-8 UTF-8/' /etc/locale.gen \
    && locale-gen \
    && rm -rf /var/lib/apt/lists/*

ENV TZ=Pacific/Tahiti
ENV LANG=fr_FR:UTF-8
ENV LANGUAGE=fr
ENV LC_ALL=fr_FR.UTF-8

COPY 21/jdk/debian/install_certs-21 /tmp/install_certs
RUN bash -xe /tmp/install_certs
