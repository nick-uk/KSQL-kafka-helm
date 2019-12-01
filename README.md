# Helm Chart for a basic KSQL kubernetes stack
All-In-One helm Chart for KSQL kubernetes stack for development tests

## What is this repository for?
* Looking around I couldn't find any working & practical Helm chart to deploy easy a basic configurable Kafka - KSQL stack in my minikube or in my remote Dev Kubernetes for tests, so I created this project with only the necessary configuration options I need.
* Is using confluentinc Docker images to setup a basic Zookeeper, Kafka, schema-registry and KSQL server stack. 
* Includes 3 Kafka useful tests.

## How do I get set up?
```bash
$ helm install --name kafka --wait .
...

$ kubectl get pods
NAME                                      READY   STATUS    RESTARTS   AGE
kafka-0                                   1/1     Running   0          41m
kafka-1                                   1/1     Running   0          41m
kafka-2                                   1/1     Running   0          41m
ksql-server-85fd755d5c-8dh2q              1/1     Running   0          41m
schema-deployment-9fbbc8898-zv2b6         1/1     Running   0          41m
zookeeper-deployment-1-75c68c78f7-gbs8c   1/1     Running   0          41m

$ helm test kafka --cleanup
RUNNING: kafka-ksql-test
PASSED: kafka-ksql-test
RUNNING: kafka-produce-consume-test
PASSED: kafka-produce-consume-test
RUNNING: datagen-test
PASSED: datagen-test
...

$ kubectl port-forward $(kubectl get services -l app=ksqlserver -o name) 8088:8088
Forwarding from 127.0.0.1:8088 -> 8088
Forwarding from [::1]:8088 -> 8088
```
[![asciicast](https://asciinema.org/a/4dB6c75J492eCVQyvV3EUo1Sj.png)](https://asciinema.org/a/4dB6c75J492eCVQyvV3EUo1Sj)

## WARNING
This repo is not for production deployments. For production better use a managed service from https://www.confluent.io
