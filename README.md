# How to use ecstats for AWS Elasticache


## Pre-requisite

- Install Docker Desktop for Mac via https://hub.docker.com/editions/community/docker-ce-desktop-mac(if you are using Macbook)


```
docker version
Client: Docker Engine - Community
 Version:           19.03.5
 API version:       1.40
 Go version:        go1.12.12
 Git commit:        633a0ea
 Built:             Wed Nov 13 07:22:34 2019
 OS/Arch:           darwin/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.5
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.12
  Git commit:       633a0ea
  Built:            Wed Nov 13 07:29:19 2019
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.2.10
  GitCommit:        b34a5c8af56e510852c35414db4c1f4fa6172339
 runc:
  Version:          1.0.0-rc8+dev
  GitCommit:        3e425f80a8c931f88e6d94a8c831b9d5aa481657
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683

```
- Setup AWS ElasticCache using AWS UI

```
aws elasticache redis-demo \
--replication-group-id redis-tutorial \
--replication-group-description "Redis Cache example" \
--num-node-groups 3 \
--cache-node-type cache.t2.micro \
--cache-parameter-group default.redis5.0.cluster.on \
--engine redis \
--engine-version 5.0.6 \
--cache-subnet-group-name redis-demo-subnet ( \
--security-group-ids sg-04edf00f9703c9d04 ( \
--node-group-configuration \
"ReplicaCount=2,PrimaryAvailabilityZone='us-west-2a',ReplicaAvailabilityZones='us-west-2a','us-east-1c',Slots=-5461" \
"ReplicaCount=2,PrimaryAvailabilityZone='us-west-2a',ReplicaAvailabilityZones='us-west-2a','us-east-1a',Slots=5462-10922" \
"ReplicaCount=2,PrimaryAvailabilityZone='us-west-2a',ReplicaAvailabilityZones='us-west-2a','us-east-1b',Slots=10923-16383"
```

## Clone this Repository

```
git clone https://github.com/collabnix/ecstats
```

## Build Docker Image

```
cd ecstats
docker build -t ajeetraina/myecstats .
```

## Verifying Docker Image


```
docker images
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
ajeetraina/myecstats   latest              632036754c4f        27 minutes ago      1.25GB
ajeetraina/myecstats   v1.0                632036754c4f        27 minutes ago      1.25GB

```

## Running Docker Container


```
docker run -v$(pwd):/ecstats ajeetraina/myecstats
Grab a coffee this script takes a while...
Writing Headers
Gathering data...

```


