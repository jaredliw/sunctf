# SunCTF

## Setup

Install Docker:

```bash
sudo apt update
sudo apt install docker.io
```

```bash
docker swarm init
docker node update --label-add "name=linux-1" $(docker node ls -q)
```

```bash
git clone https://github.com/CTFd/CTFd --depth=1
cd CTFd
```

```bash
git clone https://github.com/frankli0324/CTFd-Whale CTFd/plugins/ctfd-whale --depth=1
```

```bash
docker-compose build
docker-compose up -d
```
