ARG BASE=wxsicey/openeuler:24.03-lts

FROM openeuler/openeuler:24.03-lts as builder

ARG VERSION=3.9.1

ARG TARGETARCH

# Install dependencies
RUN yum update -y && \
    yum install -y \
        gcc \
        gcc-c++ \
        make \
        cmake \
        curl \
        zlib-devel \
        bzip2-devel \
        openssl-devel \
        ncurses-devel \
        sqlite-devel \
        readline-devel \
        tk-devel \
        gdbm-devel \
        libpcap-devel \
        xz-devel \
        libev-devel \
        expat-devel \
        libffi-devel \
        systemtap-sdt-devel && \
    yum clean all && \
    rm -rf /var/cache/yum && \
    rm -rf /tmp/*

RUN VERSION_SHORT=$(echo "${VERSION}" | cut -d. -f1,2) && \
    PY_HOME=/usr/local/python${VERSION_SHORT} && \
    PY_INSTALLER_DIR=Python-${VERSION} && \
    PY_INSTALLER_TGZ=Python-${VERSION}.tgz && \
    curl -fsSL -o "/tmp/${PY_INSTALLER_TGZ}" "https://repo.huaweicloud.com/python/${VERSION}/${PY_INSTALLER_TGZ}" && \
    tar -xf /tmp/${PY_INSTALLER_TGZ} -C /tmp && \
    cd /tmp/${PY_INSTALLER_DIR} && \
    mkdir -p /${PY_HOME}/lib && \
    ./configure --prefix=${PY_HOME} --enable-shared LDFLAGS="-Wl,-rpath ${PY_HOME}/lib" && \
    make -j "$(nproc)" && \
    make altinstall && \
    rm -rf /tmp/${PY_INSTALLER_TGZ} /tmp/${PY_INSTALLER_DIR}

FROM ${BASE} AS official

ARG VERSION

COPY --from=builder /usr/local/python* /usr/local/

RUN VERSION_SHORT=$(echo "${VERSION}" | cut -d. -f1,2) && \
    echo "export PATH=/usr/local/python${VERSION_SHORT}/bin:${PATH}" >> /etc/profile && \
    echo "export PATH=/usr/local/python${VERSION_SHORT}/bin:${PATH}" >> ~/.bashrc