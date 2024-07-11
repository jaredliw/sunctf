# SunCTF

## Setup

[Install Docker](https://docs.docker.com/engine/install/ubuntu/):

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Create a single server cluster:

```bash
docker swarm init
docker node update --label-add "name=linux-1" $(docker node ls -q)
```

Clone CTFd and CTFd-whale to local:

```bash
git clone https://github.com/CTFd/CTFd --depth=1
git clone https://github.com/frankli0324/CTFd-Whale CTFd/CTFd/plugins/ctfd-whale --depth=1
```

Clone this repository and replace the files in CTFd:

```bash
git clone https://github.com/jaredliw/sunctf
cp sunctf/docker-compose.yml CTFd/
cp -r sunctf/conf/* CTFd/conf/
```

Start:

```bash
cd CTFd/
docker compose up --build -d
```
