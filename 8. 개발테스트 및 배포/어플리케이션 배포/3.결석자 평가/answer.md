# 🧪 애플리케이션 배포 능력평가 - 문제 및 정답

---

## 🧩 문제 1. EC2 환경 구성 (20점)

Amazon Linux2 EC2 서버에서 Node.js 18버전과 yarn을 설치하는 명령어를 각각 작성하고, 해당 설치가 완료되었는지 버전 확인을 위한 명령어도 작성하시오.

### ✅ 정답

```bash
curl -sL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs
npm install -g yarn
node -v
yarn -v
```

---

## 🧩 문제 2. Git 프로젝트 초기 설정 (20점)

다음 조건에 맞춰 Git 환경을 구성하는 명령어를 작성하시오.

1. Git 저장소를 로컬에 복제  
2. 작업 디렉토리 상태 확인  
3. 숨김 파일 포함 전체 목록 확인  
4. `.env` 파일에서 `PORT` 값을 출력하는 명령어  

### ✅ 정답

```bash
git clone https://github.com/사용자명/저장소명.git
git status
ls -a
grep PORT .env
```

---

## 🧩 문제 3. GitHub Actions 기본 구성 (20점)

Node.js 18 환경에서 CI를 위한 GitHub Actions 워크플로우를 구성한다고 할 때 다음을 수행하시오.

1. `.github/workflows` 디렉토리 생성  
2. Node.js 18 설치를 위한 `setup-node` 액션 작성  
3. 의존성 설치 명령 추가  
4. `npm run build` 명령 추가  

### ✅ 정답

```bash
mkdir -p .github/workflows
```

```yaml
# .github/workflows/main.yml (예시)
- name: Setup Node.js
  uses: actions/setup-node@v3
  with:
    node-version: '18'

- name: Install dependencies
  run: npm install

- name: Build
  run: npm run build
```

---

## 🧩 문제 4. 정적 파일 배포 (20점)

React 프로젝트의 `build` 폴더를 S3 버킷에 업로드하고, 해당 파일이 공개적으로 접근 가능하도록 설정하는 AWS CLI 명령어 2개를 작성하시오.

### ✅ 정답

```bash
aws s3 sync ./build s3://my-bucket-name --acl public-read
aws s3api put-object-acl --bucket my-bucket-name --key index.html --acl public-read
```

---

## 🧩 문제 5. 서비스 확인 및 복구 (20점)

배포 완료 후 서비스를 확인하고 문제가 발생했을 경우 이전 버전으로 복구하는 과정을 수행하기 위한 다음 명령어를 작성하시오.

1. `curl`을 사용하여 배포된 웹페이지의 상태 코드 확인  
2. `app_backup` 디렉토리의 내용을 원래 `app` 디렉토리로 복사하는 명령어  

### ✅ 정답

```bash
curl -I http://<배포 주소 또는 IP>
cp -r /home/ec2-user/app_backup/* /home/ec2-user/app/
```

---
