FROM jupyter/pyspark-notebook:spark-3.3.1

USER root

ARG ICEBERG_VERSION=1.3.1
ARG NESSIE_VERSION=0.67.0
ARG AWS_SDK_VERSION=2.17.178
ENV EXTRA_JAR_DIR=/opt/iceberg/jars

RUN apt-get update && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p ${EXTRA_JAR_DIR} && \
    curl -L -o ${EXTRA_JAR_DIR}/iceberg-spark-runtime-3.3_2.12-${ICEBERG_VERSION}.jar \
        https://repo1.maven.org/maven2/org/apache/iceberg/iceberg-spark-runtime-3.3_2.12/${ICEBERG_VERSION}/iceberg-spark-runtime-3.3_2.12-${ICEBERG_VERSION}.jar && \
    curl -L -o ${EXTRA_JAR_DIR}/nessie-spark-extensions-3.3_2.12-${NESSIE_VERSION}.jar \
        https://repo1.maven.org/maven2/org/projectnessie/nessie-integrations/nessie-spark-extensions-3.3_2.12/${NESSIE_VERSION}/nessie-spark-extensions-3.3_2.12-${NESSIE_VERSION}.jar && \
    curl -L -o ${EXTRA_JAR_DIR}/bundle-${AWS_SDK_VERSION}.jar \
        https://repo1.maven.org/maven2/software/amazon/awssdk/bundle/${AWS_SDK_VERSION}/bundle-${AWS_SDK_VERSION}.jar && \
    curl -L -o ${EXTRA_JAR_DIR}/url-connection-client-${AWS_SDK_VERSION}.jar \
        https://repo1.maven.org/maven2/software/amazon/awssdk/url-connection-client/${AWS_SDK_VERSION}/url-connection-client-${AWS_SDK_VERSION}.jar

ENV SPARK_EXTRA_JARS="${EXTRA_JAR_DIR}/iceberg-spark-runtime-3.3_2.12-${ICEBERG_VERSION}.jar,${EXTRA_JAR_DIR}/nessie-spark-extensions-3.3_2.12-${NESSIE_VERSION}.jar,${EXTRA_JAR_DIR}/bundle-${AWS_SDK_VERSION}.jar,${EXTRA_JAR_DIR}/url-connection-client-${AWS_SDK_VERSION}.jar"
ENV PYSPARK_SUBMIT_ARGS="pyspark-shell"

USER ${NB_UID}
