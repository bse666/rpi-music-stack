FROM hypriot/rpi-alpine-scratch

ENV SIMA_VERSION 0.14.1
ENV PYTHON_VERSION 3.5.1-r0

RUN apk -q update \
    && apk -q --no-progress --no-cache add python3 ca-certificates \
    && apk -q --no-progress add curl
    
RUN curl -fsSl http://media.kaliko.me/src/sima/releases/MPD_sima-$SIMA_VERSION.tar.xz -o sima.tar.xz \
    && tar -xJf sima.tar.xz \
    && rm -rf sima.tar.xz \
    && sed -i 's,https://raw.github.com/pypa/pip/master/contrib/get-pip.py,https://bootstrap.pypa.io/get-pip.py,g' MPD_sima-$SIMA_VERSION/vinstall.py \
    && python3 MPD_sima-$SIMA_VERSION/vinstall.py \
    && apk -q --no-progress del curl \
    && rm -rf /var/cache/apk/*

COPY sima.conf /MPD_sima-$SIMA_VERSION/sima.conf
WORKDIR MPD_sima-$SIMA_VERSION

CMD ["./vmpd-sima", "-c", "sima.conf"]
