FROM eclipse-temurin:17-jre-jammy

LABEL govpf.category="runtime"
LABEL govpf.fromimage="eclipse-temurin:17-jre-jammy"

ENV TZ=Pacific/Tahiti

RUN apt-get update && apt-get install -y --no-install-recommends locales curl \
    && sed -i -e 's/# fr_FR.UTF-8 UTF-8/fr_FR.UTF-8 UTF-8/' /etc/locale.gen \
    && locale-gen \
    && echo "$TZ" > /etc/timezone \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata \
    && rm -rf /var/lib/apt/lists/*

ENV LANG=fr_FR:UTF-8
ENV LANGUAGE=fr
ENV LC_ALL=fr_FR.utf8

COPY install_certs /tmp/install_certs
RUN sh /tmp/install_certs

# CVE-2026-91403 : blocage des CA intermédiaires eMudhra compromises
COPY emudhra-blocked.certs /tmp/emudhra-blocked.certs
RUN set -e \
 && f=$(find "$JAVA_HOME" -name blocked.certs -o -name blacklisted.certs | head -n1) \
 && test -n "$f" \
 && echo >> "$f" \
 && cat /tmp/emudhra-blocked.certs >> "$f" \
 && grep -q 42C4ACCD12C4F59597925E1A08A7A90102608543809308D50EC427E118BA1493 "$f" \
 && rm /tmp/emudhra-blocked.certs