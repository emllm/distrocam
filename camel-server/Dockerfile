FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Install required packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    openjdk-11-jre-headless \
    groovy \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

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
