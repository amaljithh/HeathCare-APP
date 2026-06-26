FROM eclipse-temurin:17-jre-jammy
WORKDIR /app

ARG OTEL_VERSION=1.31.0
ARG OTEL_AGENT_JAR=opentelemetry-javaagent.jar
ADD https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v${OTEL_VERSION}/${OTEL_AGENT_JAR} /app/${OTEL_AGENT_JAR}

COPY target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["sh", "-c", "exec java $JAVA_TOOL_OPTIONS -jar /app/app.jar"]