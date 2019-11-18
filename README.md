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
      
      
Important!
Set properly timezone.
In beta version we tested it only with Europe/Moscow timezone.
      - TZ=Europe/Moscow
Please tell me if Your timezone work inproperly


PS:
It is beta version and not have rich feature, You can find data by any field and filter it use severity (if You enter 3 - You get 3,2,1 and 0 severity)
