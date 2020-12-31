# Docker LNMP environment

# Usage
clone
```
git clone https://github.com/BrooksYang/docker-lnmp.git
```

env
```
cp .env.example .env
```

nginx sites
```
cd nginx/sites
cp default.conf xxx.conf # config your nginx sites
```

run
```
docker-compose up -d
```

reload nginx
```
docker exec -it [nginx contianer id/name]  nginx -s reload
```

or
```
# exec nginx container
docker exec -it [nginx container id/name] bash

# reload nginx
nginx -s reload
```
