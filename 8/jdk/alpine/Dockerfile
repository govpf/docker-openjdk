FROM eclipse-temurin:8-jdk-alpine

LABEL govpf.category="runtime"
LABEL govpf.fromimage="eclipse-temurin:8-jdk-alpine"
# Timezone
ENV TZ Pacific/Tahiti
RUN apk add --no-cache ca-certificates curl tzdata wget \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo "$TZ" > /etc/timezone

# Locale
ENV LANG=fr_FR:UTF-8
ENV LANGUAGE=fr
ENV LC_CTYPE=fr_FR.utf8
ENV LC_MESSAGES=fr_FR.utf8
ENV LC_ALL=fr_FR.utf8

ENV MUSL_LOCALE_DEPS="cmake make musl-dev gcc gettext-dev libintl"
ENV MUSL_LOCPATH="/usr/share/i18n/locales/musl"
RUN apk add --no-cache $MUSL_LOCALE_DEPS \
    && wget https://github.com/govpf/musl-locales/archive/master.zip \
    && unzip master.zip \
    && cd musl-locales-master \
    && cmake -DCMAKE_POLICY_VERSION_MINIMUM=3.5 -DLOCALE_PROFILE=OFF -DCMAKE_INSTALL_PREFIX:PATH=/usr . && make && make install \
    && cd .. && rm -r musl-locales-master

# Certs
COPY install_certs /tmp/install_certs
RUN  apk add --no-cache bash && bash -xe /tmp/install_certs

# CVE-2026-91403 : blocage des CA intermédiaires eMudhra compromises
COPY emudhra-blocked.certs /tmp/emudhra-blocked.certs
RUN set -e \
 && f=$(find "$JAVA_HOME" -name blocked.certs -o -name blacklisted.certs | head -n1) \
 && test -n "$f" \
 && echo >> "$f" \
 && cat /tmp/emudhra-blocked.certs >> "$f" \
 && grep -q 42C4ACCD12C4F59597925E1A08A7A90102608543809308D50EC427E118BA1493 "$f" \
 && rm /tmp/emudhra-blocked.certs
