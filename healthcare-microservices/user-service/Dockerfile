FROM eclipse-temurin:17-jre-jammy
WORKDIR /app

ARG OTEL_VERSION=1.31.0
ARG OTEL_AGENT_JAR=opentelemetry-javaagent.jar
ADD https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v${OTEL_VERSION}/${OTEL_AGENT_JAR} /app/${OTEL_AGENT_JAR}

COPY target/*.jar app.jar

ENV SERVICE_NAME=user-service
ENV OTEL_EXPORTER_OTLP_ENDPOINT=${OTEL_EXPORTER_OTLP_ENDPOINT:-http://otel-collector:4317}
ENV OTEL_TRACES_EXPORTER=otlp
ENV OTEL_METRICS_EXPORTER=otlp
ENV OTEL_RESOURCE_ATTRIBUTES=service.name=${SERVICE_NAME}
ENV JAVA_TOOL_OPTIONS="-javaagent:/app/${OTEL_AGENT_JAR} ${JAVA_TOOL_OPTIONS:-}"

EXPOSE 8080
ENTRYPOINT ["sh", "-c", "exec java $JAVA_TOOL_OPTIONS -jar /app/app.jar"]