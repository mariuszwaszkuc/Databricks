FROM apache/spark:3.5.1

# -- Metadata
ARG build_date
LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.name="JupyterLab with PySpark, Delta and Pandas"
LABEL org.label-schema.description="JupyterLab image"


# -- Python packages + build tools
ARG delta_spark_version=3.2.0
ARG deltalake_version=0.10.0
ARG pandas_version=2.0.3
ARG jupyterlab_version=4.2.5
ARG sparksql_magic_version=0.0.3
ARG kafka_python_version=2.2.15
USER root
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends python3-pip python3-dev build-essential g++ cmake cargo libssl-dev libffi-dev wget git && \
    pip3 install --no-cache-dir \
        delta-spark==${delta_spark_version} \
        deltalake==${deltalake_version} \
        pandas==${pandas_version} \
        jupyterlab==${jupyterlab_version} \
        sparksql-magic==${sparksql_magic_version} \
        kafka-python==${kafka_python_version} && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 8888

ENV SHARED_WORKSPACE=/opt/workspace
WORKDIR ${SHARED_WORKSPACE}

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]
