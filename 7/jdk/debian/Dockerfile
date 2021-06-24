FROM openjdk:7u221-jdk-jessie

COPY install_certs /tmp/install_certs
RUN sh /tmp/install_certs

ENV TZ Pacific/Tahiti

RUN apt-get update && apt-get install -y --no-install-recommends locales \
    && sed -i -e 's/# fr_FR.UTF-8 UTF-8/fr_FR.UTF-8 UTF-8/' /etc/locale.gen \
    && locale-gen \
    && echo "$TZ" > /etc/timezone \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata \
    && rm -rf /var/lib/apt/lists/*

ENV LANG fr_FR:UTF-8
ENV LANGUAGE fr
ENV LC_ALL fr_FR.utf8
