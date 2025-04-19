##### mysql-pvc가 mysql-pv 실습을 위해서 /mnt/data/mysql 경로는 테스트 환경에서 존재해야 하며, 필요 시 수동 생성:
sudo mkdir -p /mnt/data/mysql
sudo chmod 777 /mnt/data/mysql

##### springboot-deployment.yaml에서 docker image 경로 지정 확인(docker hub id/image name:version)
```
 containers:
      - name: springboot-app
        image: wyhwang/spboot_app_jdk21:latest  # 빌드 후 Docker Hub에 올려야 함
        ports:
        - containerPort: 8080
```

##### 실행 순서
kubectl apply -f mysql-volume.yaml

kubectl apply -f mysql-deployment.yaml

kubectl apply -f mysql-service.yaml

kubectl apply -f springboot-deployment.yaml

kubectl apply -f springboot-service.yaml

##### 확인
kubectl get svc springboot-app
```
NAME             TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
springboot-app   NodePort   10.107.99.89   <none>        8087:30810/TCP   2m52s
```

curl http://192.168.56.61:30810
```
Hello from Spring Boot with OpenJDK 21 and MySQL!root@master:~/kopoDockerPractice/springboot-mysql-openjdk21/kubernetes
```

