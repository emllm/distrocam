FROM groovy:3.0-jdk11

# Set working directory
WORKDIR /app

# Install required packages with non-interactive frontend
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    python3 \
    python3-pip \
    unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip3 install -r requirements.txt

# Copy Groovy scripts
COPY src/ /app/src/

# Create deployment directory
RUN mkdir -p /app/deployment

# Set the entrypoint
ENTRYPOINT ["groovy", "-cp", "/app/src", "src/main/groovy/ClientAgent.groovy"]
