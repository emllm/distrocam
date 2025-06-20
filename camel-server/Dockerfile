FROM groovy:3.0-jdk11

# Set working directory
WORKDIR /app

# Install required packages with non-interactive frontend
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    python3 \
    python3-pip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip3 install -r requirements.txt

# Create config directory
RUN mkdir -p /app/config

# Copy Groovy scripts and config
COPY src/ /app/src/
COPY ../config/ /app/config/

# Download Apache Camel Kamelets if needed
# RUN mkdir -p /app/kamelets && \
#     curl -L https://repo1.maven.org/maven2/org/apache/camel/kamelets/camel-kamelets-utils/0.9.0/camel-kamelets-0.9.0-utils.tar.gz | \
#     tar xz -C /app/kamelets

# Set the entrypoint
ENTRYPOINT ["groovy", "-cp", "/app/src:/app/config", "src/main/groovy/EmailProcessor.groovy"]
