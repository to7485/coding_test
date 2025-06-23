## ✅ 문제 1. 배포 환경 구성 명령어 작성 (25점)

### 정답

1. `sudo dnf install java-17-amazon-corretto -y`  
2. `sudo dnf install git -y`  
3. `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`  
4. `cat ~/.ssh/id_rsa.pub`  
5. `sudo ufw status` 또는 `ss -tuln`


## ✅ 문제 2. 소스코드 검증 명령어 작성 (20점)

### 정답

1. `git clone https://github.com/사용자명/저장소명.git`  
2. `ls -a`  
3. `cat src/main/resources/application.properties` 또는 `cat application.yml`  
4. `./gradlew dependencies` 또는 `mvn dependency:tree`  
5. `./gradlew -v` 또는 `mvn -v`

## ✅ 문제 3. GitHub Actions 빌드 명령어 작성 (30점)

### 정답

1. `mkdir -p .github/workflows`  

2. 
```yaml
- name: Set up JDK 17
  uses: actions/setup-java@v3
  with:
    java-version: '17'
    distribution: 'corretto'
```

3. 
```yaml
- name: Build with Gradle
  run: ./gradlew build
```

4. GitHub 저장소 → Actions 탭에서 확인  

5. `ls build/libs` 또는 `ls target`  

6. GitHub Actions에서 `checkout` → `Java 설치` → `build` 순으로 실행하여 `.jar` 파일을 자동 생성함

## ✅ 문제 4. 배포 및 복구 명령어 작성 (25점)

1. `scp -i key.pem build/libs/app.jar ec2-user@<EC2_IP>:/home/ec2-user/app/`  
2. `ssh -i key.pem ec2-user@<EC2_IP>`  
3. `java -jar /home/ec2-user/app/app.jar`  
4. `curl http://localhost:8080` 또는 `curl http://<EC2_IP>:8080`  
5. `cp /home/ec2-user/app/app_backup.jar /home/ec2-user/app/app.jar`