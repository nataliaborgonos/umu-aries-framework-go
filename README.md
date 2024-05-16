# Moded Aries-Framework-Go

Aries Agent with modification for:

- Use dp-abc crypto
- Use vdr fabric for hyperledger fabric as verfiable storage
- Simplified Demo
- Usage example
## Requisites
- Docker-compose 1.28.5+

```
curl -L https://github.com/docker/compose/releases/download/1.28.5/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

- JQ command

```
apt install jq
```

## Get

To obtain the repo with submodules run clone like this:

```
git clone -c http.sslVerify=false https://ants-gitlab.inf.um.es/agusmf/umu-aries-framework-go.git
cd umu-aries-framework-go
git -c http.sslVerify=false submodule  update --init --recursive
```

## Run With Hyperledger Farbic

There are new Make Rules related to the deployment of Hyperledger Fabric:

- build-fabric
- run-fabric
- stop-fabric
- restart-fabric # TODO include and test

To run this mod aries-framework-go which uses a basic vdr to connect with Hyperledger Fabric, first of all and only once, you need to run: `make build-fabric`. It will download docker and resources needed to ./modules/fabric-samples.

### Deploy agent

The new Fabric VDR is automatically added by default. Besides, the rules related to launching de Aries Demo `run-openapi-demo` were modified in order to run hyperledger fabric automatically with the necessary rules.

```
run-openapi-demo: stop-openapi-demo generate-test-keys generate-dpabc-clib run-fabric generate-openapi-demo-specs
```

So, doing `make run-openapi-demo` will now, stop it, generate dp-abc C libraries and run Hyperledger Fabric deployment, already with an SmartContract installed. See scripts `./scripts/fabric/*`

`NOTE:` if you have problems deploying everything and errors appears, may is a problem related to volumes or containers that didn't get correctly stopped, so try:

```
make clean
make stop-openapi-demo
```

Before running `make run-openapi-demo`
