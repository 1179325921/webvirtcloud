# Setup HubGridCloud
### Requirements for hypervisor:
* docker 18.06
* vagrant 2.x
* VirtualBox 5.x

## Setup dev environment

### Docker compose
Build and run docker-compose (run only first time)
```bash
docker-compose up -d
docker exec -it $(docker-compose ps -q mariadb) \
       mysql -uroot -proot -e "CREATE DATABASE webvirtcloud CHARACTER SET utf8 COLLATE utf8_general_ci"
docker exec -it $(docker-compose ps -q backend) python3.6 manage.py migrate
```

Stop docker-compose
```bash
docker-compose stop
```

Start docker-compose
```bash
docker-compose start
```

Delete docker-compose
```bash
docker-compose down
```

Rebuild app container for new requirements
```bash
docker-compose up -d --no-deps --build backend
```

### Scripts for running services
Run stmpd dev server
```bash
devenv/docker/exec_backend_smtpd.sh
```

### Vagrant
Deploy dev hypervisor (run only first time)
```bash
vagrant up --provider=virtualbox
```

Run dev hypervisor
```bash
vagrant up
```

Stop dev hypervisor
```bash
vagrant halt
```
