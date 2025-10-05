# docker/spark-base/Dockerfile
FROM apache/spark:3.5.1

# -- Layer: Image Metadata
ARG build_date
ARG delta_package_version
ARG spark_xml_package_version

LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.description="Data Engineering with Apache Spark and Delta Lake Cookbook - Spark base image"
LABEL org.label-schema.schema-version="1.0"

# -- Środowisko Python + Delta
ARG delta_spark_version
ARG deltalake_version
ARG pandas_version

USER root
RUN apt-get update -y && apt-get install -y --no-install-recommends python3-pip python3-dev && \
    pip install --no-cache-dir \
        delta-spark==${delta_spark_version} \
        deltalake==${deltalake_version} \
        pandas==${pandas_version} && \
    rm -rf /var/lib/apt/lists/*

# -- Ustawienia Spark
ENV SPARK_HOME=/opt/spark
ENV SPARK_MASTER_HOST=spark-master
ENV SPARK_MASTER_PORT=7077
ENV PYSPARK_PYTHON=python3

# -- Tworzenie użytkownika
ARG NBuser=NBuser
ARG GROUP=NBuser
RUN groupadd -r ${GROUP} && useradd -r -m -g ${GROUP} ${NBuser}
ENV SHARED_WORKSPACE=/opt/workspace
RUN mkdir -p ${SHARED_WORKSPACE}/data && chown -R ${NBuser}:${GROUP} ${SHARED_WORKSPACE} ${SPARK_HOME}

USER ${NBuser}
WORKDIR ${SPARK_HOME}

# -- Opcjonalnie ustawienie aliasów
RUN echo "alias pyspark='${SPARK_HOME}/bin/pyspark'" >> ~/.bashrc && \
    echo "alias spark-shell='${SPARK_HOME}/bin/spark-shell'" >> ~/.bashrc

# -- Jary dodatkowe (Delta, XML, Kafka) w razie potrzeby
ENV SPARK_JARS_PACKAGES="io.delta:${delta_package_version},com.databricks:${spark_xml_package_version},org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.1"

CMD ["bash"]
