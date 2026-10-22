FROM eclipse-temurin:11-jre-alpine

LABEL govpf.category="runtime"
LABEL govpf.fromimage="eclipse-temurin:11-jre-alpine"

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
    && cmake -DCMAKE_POLICY_VERSION_MINIMUM=3.5 -DLOCALE_PROFILE=OFF -DCMAKE_INSTALL_PREFIX:PATH=/usr . && make && make install \
    && cd .. && rm -r musl-locales-master \
    && apk del ${MUSL_LOCALE_DEV_DEPS}

ENV TZ=Pacific/Tahiti
ENV LANG=fr_FR:UTF-8
ENV LANGUAGE=fr
ENV LC_ALL=fr_FR.UTF-8

COPY install_certs /tmp/install_certs
RUN bash -xe /tmp/install_certs

# CVE-2026-91403 : blocage des CA intermédiaires eMudhra compromises
COPY emudhra-blocked.certs /tmp/emudhra-blocked.certs
RUN set -e \
 && f=$(find "$JAVA_HOME" -name blocked.certs -o -name blacklisted.certs | head -n1) \
 && test -n "$f" \
 && echo >> "$f" \
 && cat /tmp/emudhra-blocked.certs >> "$f" \
 && grep -q 42C4ACCD12C4F59597925E1A08A7A90102608543809308D50EC427E118BA1493 "$f" \
 && rm /tmp/emudhra-blocked.certs