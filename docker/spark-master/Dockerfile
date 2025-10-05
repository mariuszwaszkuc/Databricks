FROM apache/spark:3.5.1

# -- Metadata
ARG build_date
LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.description="Spark Master with Delta and Pandas"
LABEL org.label-schema.schema-version="1.0"

# -- Python + Delta + Pandas + build tools
ARG delta_spark_version=3.2.0
ARG deltalake_version=0.10.0
ARG pandas_version=2.0.3
USER root
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends python3-pip python3-dev build-essential g++ cmake cargo libssl-dev libffi-dev && \
    pip3 install --no-cache-dir \
        delta-spark==${delta_spark_version} \
        deltalake==${deltalake_version} \
        pandas==${pandas_version} && \
    rm -rf /var/lib/apt/lists/*

# -- Env
ENV SPARK_MASTER_HOST=spark-master
ENV SPARK_MASTER_PORT=7077
ENV PYSPARK_PYTHON=python3

EXPOSE 8080 7077

CMD ["/opt/spark/bin/spark-class", "org.apache.spark.deploy.master.Master"]
