```sh
version: '3'

services:

  keycloak:
     image: quay.io/keycloak/keycloak:latest
     container_name: keycloak
     restart: always
     ports:
      - 80:8080 # Listen to HTTP on host port 80 and forward to keycloak on 8080
      - 443:8443 # Listen to HTTPS on host port 443 and forward to keycloak on 8443
     
     volumes:
       - "./certs/fullchain.pem:/etc/x509/https/tls.crt"   # Map certificate to container
       - "./certs/privkey.pem:/etc/x509/https/tls.key"   # Map private key to container
       
     environment:
       #- JAVA_OPTS_APPEND="-D keycloak.profile.feature.upload_script=enabled"
       - KEYCLOAK_ADMIN_USER=admin # Change the username!
       - KEYCLOAK_ADMIN_PASSWORD=password # Change the password!
       - KC_HOSTNAME=fqdn # Set the hostname here
       - KC_HTTPS_CERTIFICATE_FILE=/etc/x509/https/tls.crt
       - KC_HTTPS_CERTIFICATE_KEY_FILE=/etc/x509/https/tls.key
    command:
       - start-dev # Start Keycloak in developer mode     
```
