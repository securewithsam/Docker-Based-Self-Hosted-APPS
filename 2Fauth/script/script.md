
```bash
#!/bin/bash

# Update package list
sudo apt update && upgrade -y

# Install necessary dependencies
sudo apt install -y php curl

# Install Docker
if ! command -v docker &> /dev/null; then
  echo "Installing Docker..."
  curl -fsSL https://get.docker.com -o get-docker.sh
  sh get-docker.sh
  rm get-docker.sh
else
  echo "Docker is already installed."
fi

# Install Docker Compose
if ! command -v docker-compose &> /dev/null; then
  echo "Installing Docker Compose..."
  sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
else
  echo "Docker Compose is already installed."
fi

# Create directories
echo "Creating necessary directories..."
mkdir -p /root/docker/2fauth/2fauth_data/database

# Set permissions
echo "Setting directory permissions..."
sudo chown -R 0:0 /root/docker/2fauth/2fauth_data
sudo chmod -R 777 /root/docker/
sudo chmod -R 777 /root/docker/2fauth/
sudo chmod -R 777 /root/docker/2fauth/2fauth_data/
sudo chmod -R 777 /root/docker/2fauth/2fauth_data/database/

# Create the docker-compose.yml file
DOCKER_COMPOSE_FILE="/root/docker/2fauth/docker-compose.yml"
echo "Creating docker-compose.yml file..."
cat <<EOL > "$DOCKER_COMPOSE_FILE"
version: "3"
services:
  2fauth:
    image: 2fauth/2fauth
    container_name: 2fauthrpi3
    volumes:
      - /root/docker/2fauth/2fauth_data:/2fauth
    ports:
      - 8093:8000/tcp # Change this to a port you wish to use
    environment:
      - APP_NAME=2FAuth
      - APP_ENV=local
      - APP_DEBUG=false
      - SITE_OWNER=sws2@gmail.com
      - APP_KEY=11wD8dV2Ewo5wMJJgODJqzS1I7Bx3RXeOnqqhSQwkoE=
      - APP_URL=http://10.0.100.62:8093
      - ASSET_URL=http://10.0.100.62:8093
      - IS_DEMO_APP=false
      - LOG_CHANNEL=daily
      - LOG_LEVEL=notice
      - DB_DATABASE="/2fauth/database/database.sqlite"
      - CACHE_DRIVER=file
      - SESSION_DRIVER=file
      - MAIL_DRIVER=smtp
      - MAIL_HOST=smtp.gmail.com
      - MAIL_PORT=587
      - MAIL_USERNAME=sws@gmail.com
      - MAIL_PASSWORD=frtg haja dsju iopl
      - MAIL_ENCRYPTION=tls
      - MAIL_FROM_NAME=2FAuth
      - MAIL_FROM_ADDRESS=sws@gmail.com
      - MAIL_VERIFY_SSL_PEER=true
      - THROTTLE_API=60
      - LOGIN_THROTTLE=5
      - AUTHENTICATION_GUARD=web-guard
      - WEBAUTHN_NAME=2FAuth
      - WEBAUTHN_USER_VERIFICATION=preferred
      - TRUSTED_PROXIES=null
      - PROXY_FOR_OUTGOING_REQUESTS=null
      - BROADCAST_DRIVER=log
      - QUEUE_DRIVER=sync
      - SESSION_LIFETIME=120
      - REDIS_HOST=127.0.0.1
      - REDIS_PASSWORD=null
      - REDIS_PORT=6379
EOL

# Start Docker Compose
echo "Starting Docker Compose..."
cd /root/docker/2fauth || exit
docker-compose up -d

echo "Setup completed successfully."
```

### How to Use
1. Save the script as `setup_2fauth.sh`.
2. Grant execute permissions to the script:
   ```bash
   chmod +x setup_2fauth.sh
   ```
3. Run the script with superuser privileges:
   ```bash
   sudo bash setup_2fauth.sh
   ```
This script will install Docker and Docker Compose, create the required directories with appropriate permissions, set up the `docker-compose.yml` file, and start the container.
