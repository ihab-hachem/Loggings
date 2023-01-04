  
## Setup



### 2. Run docker-compose:
```sh
$ docker compose up --build -d
```


### 3. After the build is done:
The services will be running at these ports:
| Container | Port |
|--|--|
Setup| -- |
Kibana| 5651 |
Logstash| 50000 |
Elasticsearch| 9250 |
Filebeat| -- |

### 4. Logging from python:
```python
from logstash import TCPLogstashHandler
import logging

logger = logging.getLogger("Gateway")
logger.setLevel(logging.INFO)

logger.addHandler(TCPLogstashHandler(
    host="localhost", 
    port=50000,
    version=1,
    fqdn=False,
    tags=["gateway"]
))

logger.error("This is an error.")
logger.warning("This is a warning.")
logger.info("This is some info.")

```