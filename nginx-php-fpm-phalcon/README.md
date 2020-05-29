## Quick Start


### Build an image (--build-arg http_proxy=xxx.xx.xxx.xx)   
```
docker build -t lemon1989/nginx-php-fpm:latest .
```

### Running

```
docker run -d -p 8080:80 4433:443 --name my-nginx lemon1989/nginx-php-fpm:latest

```

### View php

```
docker exec -it my-nginx which php
```

