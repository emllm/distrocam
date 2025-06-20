FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Install required packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    unzip \
    openjdk-11-jre-headless \
    groovy \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY client-agent/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy Groovy scripts
COPY client-agent/src/ /app/src/

# Create deployment directory
RUN mkdir -p /app/deployment

# Set the entrypoint
ENTRYPOINT ["groovy", "-cp", "/app/src", "src/main/groovy/ClientAgent.groovy"]
