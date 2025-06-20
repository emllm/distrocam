FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Install required packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first to leverage Docker cache
COPY bot-generator/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the bot script
COPY bot-generator/bot.py .

# Make the script executable
RUN chmod +x bot.py

# Run the bot
CMD ["python3", "bot.py"]
