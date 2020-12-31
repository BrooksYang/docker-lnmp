# Docker LNMP environment

## Usage
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

## Reload nginx
reload by docker-compose
```
docker-compose exec nginx nginx -s reload
```

reload by docker
```
docker exec [nginx contianer id/name]  nginx -s reload
```

or
```
# exec nginx container
docker exec -it [nginx container id/name] bash

# reload nginx
nginx -s reload
```
