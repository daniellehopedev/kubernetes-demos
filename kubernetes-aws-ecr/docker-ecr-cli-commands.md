### print password for docker login to use for aws ecr
```
aws ecr get-login-password --region <aws-ecr-region>
```

### login to docker private repo
```
docker login -u username -p password <private-repo-endpoint>
```

### generated config file from the docker login
```
cat .docker/config.json
cat .docker/config.json | base64
```

### create docker login secret from config.json file
```
kubectl create secret generic my-registry-key --from-file=.dockerconfigjson=.docker/config.json --type=kubernetes.io/dockerconfigjson

kubectl get secret
```

### create docker login secret with login credentials
```
kubectl create secret docker-registry my-registry-key --docker-server=http://private-repo --docker-username=user --docker-password=pwd
```

### access minkube console
```
minikube ssh
```

### copy config.json file from Minikube to my host
```
scp -i $(minikube ssh-key) docker@$(minikube ip):.docker/config.json .docker/config.json
# depending on your minikube version you may have to use the below
minikube cp minikube:/home/docker/.docker/config.json <home-directory>/.docker/config.json
```