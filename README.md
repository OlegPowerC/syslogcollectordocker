# syslogcollectordocker
SYSLOG collector + RESTAPI + Web GUI + mongo storage

Edit docker-compose.yaml, mongo section for persistent mongo daabase like this:
    image: mongo
    environment:
      - MONGO_DATA_DIR=/data/db
      - MONGO_LOG_DIR=/dev/null
    volumes:
      - ./data/db:/data/db
      
      
Edit syslogcollector section, if You need not regular SYSLOG UDP port
    ports:
      - 514:514/udp
 

Edit Syslogapi section, if You want change WEB GUI port, different from 80

  syslogapi:
    image: ciscoliveru/syslogapi
    environment:
      MONGOURL: mongodb://mongo:27017
    depends_on:
      - mongo
    ports:
      - 8181:80
