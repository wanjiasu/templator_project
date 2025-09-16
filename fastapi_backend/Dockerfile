FROM python:3.12-bookworm

# Set the working directory
WORKDIR /app

# Ensure certificates for TLS (pip downloads) and fix apt Post-Invoke issue
RUN set -eux; \
    rm -f /etc/apt/apt.conf.d/docker-clean || true; \
    apt-get update; \
    apt-get install -y --no-install-recommends ca-certificates; \
    rm -rf /var/lib/apt/lists/*

# Copy dependency file first to leverage Docker layer caching
COPY requirements.txt ./

# Install Python dependencies with pip (avoid downloading uv at build time)
RUN python -m pip install --no-cache-dir --upgrade pip setuptools wheel && \
    pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .

# Expose the application port
EXPOSE 8000

# Command to run the application (dev). In production, docker-compose overrides with uvicorn.
CMD ["./start.sh"]