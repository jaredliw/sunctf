<p align="center">
    <img src="/logo.png" alt="SunCTF logo" width="300">
</p>

<h3 align="center">SunCTF 2024</h3>

<p align="center">
  A CTF hosted by Sunway Cyber Security Club (CSC).
</p>

## Setup

The instructions were tested and ran on Ubuntu. Alternatively, using WSL on Windows will work as well.

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
sudo gpasswd -a $USER docker
```

Create a single server cluster:

```bash
docker swarm init
docker node update --label-add "name=linux-1" $(docker node ls -q)
```

Clone CTFd and CTFd-whale to local:

```bash
wget https://github.com/CTFd/CTFd/archive/refs/tags/3.7.3.tar.gz
tar -xzvf 3.7.3.tar.gz
mv CTFd-3.7.3/ CTFd/
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

In the admin panel, set values as in `whale.config.json`.

## Challenges

The challenges are in [Wowiee3/SunwayCTF-challs](https://github.com/Wowiee3/SunwayCTF-challs/tree/d0ced6536026c30d99367b7b6773ecda3032fa29).
Docker images for dynamic challenges are [here](https://hub.docker.com/u/jaredliw).

## Archive

To revert the system to its state at the end of the competition, go to the admin panel and import the
ZIP file located in the `archive/` folder.