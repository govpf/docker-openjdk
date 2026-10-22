FROM eclipse-temurin:26-jre-alpine

LABEL govpf.category="runtime"
LABEL govpf.fromimage="eclipse-temurin:26-jre-alpine"

RUN apk add -U --no-cache curl bash && apk upgrade --no-cache

ENV TZ=Pacific/Tahiti
ENV LANG=fr_FR:UTF-8
ENV LANGUAGE=fr
ENV LC_ALL=fr_FR.UTF-8

COPY install_certs-21 /tmp/install_certs
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
