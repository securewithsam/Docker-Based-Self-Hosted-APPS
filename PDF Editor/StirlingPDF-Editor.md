
```sh
mkdir docker 
cd docker
mkdir stirling-pdf
cd stirling-pdf
mkdir trainingData
mkdir extraConfigs
cd trainingData
```
Download the language pack 

```sh
wget https://github.com/tesseract-ocr/tessdata/blob/main/eng.traineddata
```
Go back to  stirling-pdf folder 

```sh
nano docker-compose.yml
```
paste the below

```sh
version: '3.3'
services:
  stirling-pdf:
    image: frooodle/s-pdf:latest
    ports:
      - '8060:8080'  
    volumes:
      - ./trainingData:/usr/share/tessdata #Required for extra OCR languages
      - ./extraConfigs:/configs
#      - /location/of/customFiles:/customFiles/
#      - ./logs:/logs/
    environment:
      - DOCKER_ENABLE_SECURITY=false
      - INSTALL_BOOK_AND_ADVANCED_HTML_OPS=false
      - LANGS=en_US
```


```sh
docker-compose pull
```

```sh
docker-compose up -d && docker-compose logs -f
```

http://IP:8060
