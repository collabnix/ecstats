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
##  Setup AWS ElasticCache using AWS UI

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
MacBook-Pro ecstats % docker run -v$(pwd):/ecstats ajeetraina/myecstats
Grab a coffee this script takes a while...
Writing Headers
Gathering data...

```

```
ajeetraina@Shahars-MacBook-Pro ecstats % cat production-us-west-2.csv 
,ClusterId,NodeId,NodeType,Region,CurrItems (max over last week),BytesUsedForCache (max over last week),CacheHits (max over last week),CacheMisses (max over last week),CurrConnections (max over last week),NetworkBytesIn (max over last week),NetworkBytesOut (max over last week),NetworkPacketsIn (max over last week),NetworkPacketsOut (max over last week),EngineCPUUtilization (max over last week),Evictions (max over last week),ReplicationBytes (max over last week),ReplicationLag (max over last week),GetTypeCmds (peak last week / hour),HashBasedCmds (peak last week / hour),HyperLogLogBasedCmds (peak last week / hour),KeyBasedCmds (peak last week / hour),ListBasedCmds (peak last week / hour),SetBasedCmds (peak last week / hour),SetTypeCmds (peak last week / hour),SortedSetBasedCmds (peak last week / hour),StringBasedCmds (peak last week / hour),StreamBasedCmds (peak last week / hour),Unnamed: 27
0,redis-demo,redis-demo-0001-001,cache.t2.micro,us-west-2a,0,6471376.0,0,0,4.0,33976115.0,1165917.0,23256.0,9613.0,0.2000666888962988,0,3264.0,0.0,0,0,0,0,0,0,0,0,0,0,
1,redis-demo,redis-demo-0001-002,cache.t2.micro,us-west-2a,0,6412608.0,0,0,6.0,34011036.0,1240920.0,23415.0,3062.0,0.2001000500250125,0,3264.0,0.004,0,0,0,0,0,0,0,0,0,0,
2,redis-demo,redis-demo-0001-003,cache.t2.micro,us-west-2a,0,6453520.0,0,0,7.0,33974122.0,1173810.0,23295.0,919.0,0.21666666666666667,0,4670.0,24.279,0,0,0,0,0,0,0,0,0,0,
3,redis-demo,redis-demo-0002-001,cache.t2.micro,us-west-2a,0,6411512.0,0,0,5.0,33976836.0,1161247.0,23256.0,9930.0,0.21673891297099032,0,3264.0,0.0,0,0,0,0,0,0,0,0,0,0,
4,redis-demo,redis-demo-0002-002,cache.t2.micro,us-west-2a,0,6450472.0,0,0,5.0,34012740.0,1335550.0,23453.0,2877.0,0.2,0,4564.0,23.71,0,0,0,0,0,0,0,0,0,0,
5,redis-demo,redis-demo-0002-003,cache.t2.micro,us-west-2a,0,6411568.0,0,0,5.0,34018413.0,1139350.0,23614.0,3149.0,0.2001000500250125,0,4843.0,24.244,0,0,0,0,0,0,0,0,0,0,
6,redis-demo,redis-demo-0003-001,cache.t2.micro,us-west-2a,0,6427352.0,0,0,5.0,34009223.0,1155151.0,23331.0,8241.0,0.2167750541937636,0,3264.0,0.0,0,0,0,0,0,0,0,0,0,0,
7,redis-demo,redis-demo-0003-002,cache.t2.micro,us-west-2a,0,6388552.0,0,0,5.0,34042567.0,1227967.0,24213.0,2855.0,0.2,0,3264.0,0.003,0,0,0,0,0,0,0,0,0,0,
8,redis-demo,redis-demo-0003-003,cache.t2.micro,us-west-2a,0,6388552.0,0,0,5.0,33972855.0,1231179.0,23258.0,9720.0,0.21666666666666667,0,3476.0,0.001,0,0,0,0,0,0,0,0,0,0,


###Reserved Instances
Instance Type, Count, Remaining Time (days)

costs
####Total costs per month####  0.0%  
```

