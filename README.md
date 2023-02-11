# Install Elixer Validator Testnet using Docker

## Install MetaMask
On Google Chrome go to https://metamask.io/ and install the MetaMask Chrome Extension and get your Public Address & Private Address

## Deploy Vultr Server
On Vultr Deploy Server with the following specs
- Cloud Compute
- General Purpose
- Your preferred location (eg: Frankfurt)
- Ubuntu 22.04 LTS
- 1 vCPU - 2GB Memory - $10/month
- Disable IPv6
- Enter name for server
- Deploy the server


## Install Docker & docker-compose

#### SSH Into the server using PuTTY or your terminal in Mac

### Install Docker
```shell
sudo apt update -y
```

```shell
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```shell
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```shell
sudo apt update -y
```

```shell
sudo apt install docker-ce
```

```shell
sudo usermod -aG docker ${USER}
```

```shell
sudo su - ${USER}
```

```shell
sudo systemctl enable docker
```

### Install Docker Compose

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/v2.15.1/docker-compose-linux-$(uname -m)" -o /usr/local/bin/docker-compose
```
```shell
sudo chmod +x /usr/local/bin/docker-compose
```


## Setup the application

```shell
cd
mkdir -p apps/elexor-validator-docker
cd apps/elexor-validator-docker
```


#### Add your Address and Private Address from MetaMask to the environment variables
```shell
nano docker-compose.yaml
```
```yaml
version: '3'

services:
  elixir_validator:
    image: elixirprotocol/validator:testnet-1
    restart: always
    environment:
      ADDRESS: "YOUR_ADRESS_HERE"
      PRIVATE_KEY: "YOUR_PRIVATE_ADDRESS_HERE"
```

#### Start the docker container
```
docker-compose up -d
```

#### Check the logs
```
docker-compose logs -f
```

#### After a couple of minutes you will see your Public Address and Server's IP Address at https://metrics.elixir.finance/