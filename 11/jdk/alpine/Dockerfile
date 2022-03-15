FROM adoptopenjdk/openjdk11:alpine

RUN apk update && apk add tzdata curl bash && apk upgrade --no-cache

RUN cp /usr/share/zoneinfo/Pacific/Tahiti /etc/localtime
RUN rm -r /usr/share/zoneinfo/Africa && \
    rm -r /usr/share/zoneinfo/Antarctica && \
    rm -r /usr/share/zoneinfo/Arctic && \
    rm -r /usr/share/zoneinfo/Asia && \
    rm -r /usr/share/zoneinfo/Atlantic && \
    rm -r /usr/share/zoneinfo/Australia && \
    rm -r /usr/share/zoneinfo/Europe  && \
    rm -r /usr/share/zoneinfo/Indian && \
    rm -r /usr/share/zoneinfo/Mexico && \
    rm -r /usr/share/zoneinfo/America && \
    rm -r /usr/share/zoneinfo/Chile && \
    rm -r /usr/share/zoneinfo/Canada

RUN echo "Pacific/Tahiti" >  /etc/timezone

ENV TZ Pacific/Tahiti
ENV LANG fr_FR:UTF-8
ENV LANGUAGE fr
ENV LC_ALL fr_FR:UTF-8

ENV MUSL_LOCALE_DEPS cmake make musl-dev gcc gettext-dev libintl
ENV MUSL_LOCPATH /usr/share/i18n/locales/musl
RUN apk add --no-cache $MUSL_LOCALE_DEPS \
    && wget https://github.com/govpf/musl-locales/archive/master.zip \
    && unzip master.zip \
    && cd musl-locales-master \
    && cmake -DLOCALE_PROFILE=OFF -D CMAKE_INSTALL_PREFIX:PATH=/usr . && make && make install \
    && cd .. && rm -r musl-locales-master

COPY install_certs /tmp/install_certs
RUN sh /tmp/install_certs