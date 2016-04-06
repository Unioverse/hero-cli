Welcome to the CloudHero CLI! You can use our CLI to create any type of server environments or a scalable and high available container service on top of major public or private cloud providers.

A simple use case is to create a scalable and high available Docker cluster on top of your favourite cloud provider.

![CloudHero Block Architecture](/docs/ch-block.png)


## Description
CloudHero CLI is a open-source application written in python and it is build on top of [CloudHero API](https://docs.cloudhero.io)


## Install
```
git clone https://github.com/cloud-hero/hero-cli.git  
cd hero-cli
pip install -r requirements.txt
./hero
```

## Account Registration
Once installed you need to create a account. If you already have an active CloudHero account you can skip this step.
```bash
$./hero register -e my@email.com -p password -o acme 
```

## Login
In order to use CloudHero CLI you need to login.
```bash
$./hero login -e me@email.com -p password
```

## Usage examples

### Provider
In order to deploy new servers using CloudHero CLI you need to register a cloud provider.
Currently we support AWS EC2 and DigitalOcean.

##### Add DigitalOcean
```bash
$./hero provider add digital_ocean -a DO_Access_Token --name mydoprovider
```

##### Add AWS EC2
```bash
$./hero provider add ec2 -a access_key -s secret_key --name myec2provider
```

##### Delete
```bash
$./hero provider rm provider_id
```

##### List
```bash
$./hero provider ls
```

### Environment
An environment is a group (stack) of servers. You can give them any name, but we usualy call them production, staging, development.

##### Create
```bash
$./hero env create -p provider_id -l location -n name
```

Parameter | Description
--------- | -----------
provider_id | The cloud provider that you choose to spin up the nodes. Use ```$./hero provider ls ```
locations | The location where you want to spin up your servers. See below available locations
name | Name your environment. Eg. Production or Staging

Digital Ocean | Amazon EC2
------------- | ----------
Code - Name | Code - Name
ams2 - Amsterdam 2 | us-east-1 - US East (N. Virginia) |
ams3 - Amsterdam 3 | us-west-2 - US West (Oregon) |
fra1 - Frankfurt 1 | us-west-1 - US West (N. California) |
lon1 - London 1 | eu-west-1 - EU (Ireland) |
nyc1 - New York 1 | eu-central-1 - EU (Frankfurt) |
nyc2 - New York 2 | ap-southeast-1 - Asia Pacific (Singapore) |
nyc3 - New York 3 | ap-northeast-1 - Asia Pacific (Tokyo) |
sfo1 - San Francisco 1 | ap-southeast-2 - Asia Pacific (Sydney) |
sgp1 - Singapore 1 | ap-northeast-2 - Asia Pacific (Seoul) |
tor1 - Toronto 1 | sa-east-1 - South America (São Paulo) |

##### Delete
```bash
$./hero env rm environment_id
```

Parameter | Description
--------- | -----------
environment_id | 

##### List
```bash
$./hero env ls
```

### Nodes
Nodes are servers that CloudHero will provision, install packages and configure automatically for you.

##### Add
```bash
$./hero nodes add -e env_id -k package -s size --tags key1:value1,key2:value2 --name mynode
```
Below you cand find a list of available packages:
* docker
* nginx
* php
* mysql
* memcached
* redis
* mongodb
* glusterfs

##### Scale
This option allows you to horizontally scale any running node, both up and down.
####### UP
```bash
$./hero nodes scale up -e env_id --name node_that_you_want_to_scale / --tags tags_of_node(s)_that_you_want_to_sclae --count number_of_nodes 
```

####### DOWN
```bash
$./hero nodes scale down -e env_id --name node_that_you_want_to_scale / --tags tags_of_node(s)_that_you_want_to_sclae --count number_of_nodes 
```

##### Delete
```bash
$./hero nodes scale rm node_id
```

##### SSH
This option allows you to connect securely using SSH to your nodes
```bash
$./hero nodes ssh node_id
```

### Docker
You connect to any Docker Swarm cluster provisioned with CloudHero CLI or API
```bash
$./hero docker env_id

EXPORT DOCKER_HOST=tcp://ip_of_swarm_node:4000
# Run this command to configure your shell: 
# eval "$(hero docker my-env)"
```
