# Base image
ARG java_image_tag=17-jre
FROM eclipse-temurin:${java_image_tag}

# -- Metadata
ARG build_date
ARG delta_spark_version=3.2.0
ARG deltalake_version=0.10.0
ARG pandas_version=2.0.3

LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.description="Base image for Spark cluster with Python, Delta, Pandas (virtualenv)"
LABEL org.label-schema.schema-version="1.0"

# -- OS + build tools
ARG shared_workspace=/opt/workspace

USER root
RUN mkdir -p ${shared_workspace}/data && \
    mkdir -p /usr/share/man/man1 && \
    apt-get update -y && \
    apt-get install -y --no-install-recommends \
        curl \
        python3 \
        python3-venv \
        python3-dev \
        build-essential \
        g++ \
        cmake \
        cargo \
        libssl-dev \
        libffi-dev \
        netcat-openbsd \
        scala \
        manpages-dev \
        wget \
        git && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# -- Virtualenv for Python packages
ENV VENV_PATH=/opt/venv
RUN python3 -m venv ${VENV_PATH} && \
    ${VENV_PATH}/bin/pip install --upgrade pip

# -- Install Python packages in virtualenv
RUN ${VENV_PATH}/bin/pip install --no-cache-dir \
    delta-spark==${delta_spark_version} \
    deltalake==${deltalake_version} \
    pandas==${pandas_version}

# -- Environment variables
ENV PATH="${VENV_PATH}/bin:${PATH}"
ENV SCALA_HOME=/usr/share/scala
ENV PATH=${PATH}:${SCALA_HOME}/bin
ENV SHARED_WORKSPACE=${shared_workspace}

VOLUME ${shared_workspace}
CMD ["bash"]
