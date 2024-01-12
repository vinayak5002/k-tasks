# k-tasks
This repository containes docker file for the java project, kubernetes yamls for app pod and mongo pod

# Docker images
Two images generated one for the REST API pod and one for the mongo pod

Image for the app container generated using the dockerfile
```
FROM openjdk:17
CMD ["./gradlew", "clean", "bootJar"]
COPY build/libs/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
```
Default image for mongodb container was used

Both the containers communicate together through network

# Kubernetes
Kubernetes cluster was created locally using minikube  
![Screenshot 2024-01-12 102451](https://github.com/vinayak5002/k-tasks/assets/82216732/c862f6e6-db7b-4bd4-83b1-ee68b29e68b8)


Two pods were created using the yaml files present in the repo
One pod for the java app to run and one for mongodb

The storage pod ([mongo pod](https://github.com/vinayak5002/k-tasks/blob/main/db.yaml)) is made persisten using PersistentVolumeClaim
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 256Mi
```
*refer the yaml file

Both the pods are deployed using kubectl CLI  
![Screenshot 2024-01-12 102946](https://github.com/vinayak5002/k-tasks/assets/82216732/60226dd4-e66b-4385-868f-862c3a9509e1)

Status of running pods  
![Screenshot 2024-01-12 103032](https://github.com/vinayak5002/k-tasks/assets/82216732/891cbe75-4494-418e-ac6e-605f4b3e10b8)

Url for the deployed java app
![Screenshot 2024-01-12 103316](https://github.com/vinayak5002/k-tasks/assets/82216732/12a1bb96-c509-47bc-b153-9acfd9ac1e06)

Working endpoints of the app
create task POST request:
![Screenshot 2024-01-12 103712](https://github.com/vinayak5002/k-tasks/assets/82216732/a8758a6d-1eea-46e8-8331-fec46ee7aa17)

all tasks GET request:
![Screenshot 2024-01-12 104127](https://github.com/vinayak5002/k-tasks/assets/82216732/4d77da8f-ef5c-4f52-8c94-df30364b61b0)
