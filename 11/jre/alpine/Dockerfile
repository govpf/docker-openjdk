FROM adoptopenjdk/openjdk11:alpine-jre

RUN apk update && apk add tzdata curl && apk upgrade

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

COPY install_certs /tmp/install_certs
RUN sh /tmp/install_certs