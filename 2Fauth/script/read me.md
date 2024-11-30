
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
This script will update, install Docker and Docker Compose, create the required directories with appropriate permissions, set up the `docker-compose.yml` file, and start the container.


### Next -Run the command below to get a Random 32 key for DB encryption

 ```bash
sudo php -r "echo base64_encode(openssl_random_pseudo_bytes(32));"
   ```
### Update the key in the docker-compose.yml environment variable under APP_KEY
![image](https://github.com/user-attachments/assets/b1dc5c36-c49a-4951-9c14-cc78eddcda43)

### Make sure to update the APP_URL & ASSET_URL to the VM/Instance private IP (If using a cloudflare, update the domain) 
![image](https://github.com/user-attachments/assets/948c3ec3-a592-4992-b29d-2fff381ee945)


### Final Step , re pull the docker compose for changes to take effect  
cd /root/docker/2fauth

```bash
  docker-compose up -d
```

#### Troubleshooting Logs
```bash
sudo docker compose logs
sudo docker logs 2fauth
ls-al
```
