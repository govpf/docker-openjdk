FROM eclipse-temurin:11-jdk-alpine

ENV MUSL_LOCPATH=/usr/share/i18n/locales/musl

RUN MUSL_LOCALE_DEV_DEPS="cmake make musl-dev gcc gettext-dev" \
    && MUSL_LOCALE_DEPS="gettext libintl" \
    && apk add -U --no-cache tzdata curl bash gettext libintl ${MUSL_LOCALE_DEPS} ${MUSL_LOCALE_DEV_DEPS} \
    && apk upgrade --no-cache \
    && cp /usr/share/zoneinfo/Pacific/Tahiti /etc/localtime \
    && rm -r /usr/share/zoneinfo/Africa \
    && rm -r /usr/share/zoneinfo/Antarctica \
    && rm -r /usr/share/zoneinfo/Arctic \
    && rm -r /usr/share/zoneinfo/Asia \
    && rm -r /usr/share/zoneinfo/Atlantic \
    && rm -r /usr/share/zoneinfo/Australia \
    && rm -r /usr/share/zoneinfo/Europe  \
    && rm -r /usr/share/zoneinfo/Indian \
    && rm -r /usr/share/zoneinfo/Mexico \
    && rm -r /usr/share/zoneinfo/America \
    && rm -r /usr/share/zoneinfo/Chile \
    && rm -r /usr/share/zoneinfo/Canada \
    && echo "Pacific/Tahiti" > /etc/timezone \
    && apk del tzdata \
    && wget https://github.com/govpf/musl-locales/archive/master.zip \
    && unzip master.zip \
    && rm master.zip \
    && cd musl-locales-master \
    && cmake -DLOCALE_PROFILE=OFF -D CMAKE_INSTALL_PREFIX:PATH=/usr . && make && make install \
    && cd .. && rm -r musl-locales-master \
    && apk del ${MUSL_LOCALE_DEV_DEPS}

ENV TZ=Pacific/Tahiti
ENV LANG=fr_FR:UTF-8
ENV LANGUAGE=fr
ENV LC_ALL=fr_FR.UTF-8

COPY install_certs /tmp/install_certs
RUN bash -xe /tmp/install_certs