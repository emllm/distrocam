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

# Copy the bot script
COPY bot.py .

# Make the script executable
RUN chmod +x bot.py

# Run the bot
CMD ["python3", "bot.py"]
