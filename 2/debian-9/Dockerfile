FROM bitnami/minideb:stretch
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-9" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl libc6 libgcc1 libicu57 libssl1.1 libstdc++6 libtinfo5 procps unzip zlib1g
RUN . ./libcomponent.sh && component_unpack "couchdb" "2.3.1-6" --checksum 0659a09a8c04ce20dcd680068bdeea110512358c100f33693b58de71d61e708f
RUN curl --silent -L https://github.com/tianon/gosu/releases/download/1.11/gosu-amd64 > /usr/local/bin/gosu && \
    echo 0b843df6d86e270c5b0f5cbd3c326a04e18f4b7f9b8457fa497b0454c4b138d7 /usr/local/bin/gosu | sha256sum --check && \
    chmod u+x /usr/local/bin/gosu && \
    mkdir -p /opt/bitnami/licenses && \
    curl --silent -L https://raw.githubusercontent.com/tianon/gosu/master/LICENSE > /opt/bitnami/licenses/gosu-1.11.txt
RUN curl --silent -Lo /tmp/ini-file.zip https://github.com/bitnami/ini-file/releases/download/v1.0/ini-file.zip && echo 2f12cc487b0b17cf5346326ae653951e9ff6d5eb6d3c9217c602060778996b64 /tmp/ini-file.zip | sha256sum --check && unzip -q -d /usr/local/bin -o /tmp/ini-file.zip ini-file && mkdir -p /opt/bitnami/licenses && curl --silent -L https://raw.githubusercontent.com/bitnami/ini-file/master/COPYING > /opt/bitnami/licenses/ini-file-1.0.txt
RUN curl --silent -L https://github.com/bitnami/wait-for-port/releases/download/v1.0/wait-for-port.zip > /tmp/wait-for-port.zip && \
    echo "8d26181f4629211b70db4f96236616056b1ed8e5920d8023f7c883071e76c1ed /tmp/wait-for-port.zip" | sha256sum --check && \
    unzip -q -d /usr/local/bin -o /tmp/wait-for-port.zip wait-for-port && \
    mkdir -p /opt/bitnami/licenses && \
    curl --silent -L https://raw.githubusercontent.com/bitnami/wait-for-port/master/COPYING > /opt/bitnami/licenses/wait-for-port-1.0.txt

COPY rootfs /
RUN /postunpack.sh
ENV BITNAMI_APP_NAME="couchdb" \
    BITNAMI_IMAGE_VERSION="2.3.1-debian-9-r76" \
    LD_LIBRARY_PATH="/opt/bitnami/common/lib:$LD_LIBRARY_PATH" \
    PATH="/opt/bitnami/couchdb/bin:$PATH"

VOLUME [ "/bitnami/couchdb" ]

EXPOSE 5984 4369 9100

USER 1001
ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "/run.sh" ]
