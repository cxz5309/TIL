# Github Actions

![img](https://user-images.githubusercontent.com/42149645/147480102-9a50057e-227c-407c-9828-42a21b783d90.png)  

- Github CI/CD tool
- Runners 라는 Linux, macOS, Windows 환경에서 실행된다.
- Workflow는 마켓 플레이스에서 공유되어 사용 가능하다.
- public 저장소는 무료! private 저장소는 한달 500MB, 실행시간 2000분까지 무료이다.

## 장점
- 다른 CI/CD 도구에 비해 매우 쉽다.
- 따라서 레퍼런스가 많으며 다른 툴에서 넘어오는 추세라고 한다.
- github 환경 설정 불필요
- 모든 github 이벤트의 작업을 이용할 수 있고 다양한 언어와 프레임워크를 지원
- 도커 이미지가 아니더라도 호환 가능


## 사용
- 기본 push 트리거
깃허브에 push 했을 때 CI 로그 확인

```yml
# This is a basic workflow to help you get started with Actions

name: CI

on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      # Runs a single command using the runners shell
      - name: Run a one-line script
        run: echo Hello, world!

      - name: Run a multi-line script
        run: |
          echo Add other actions to build,
          echo test, and deploy your project.

      - name: Setup Node.js environment
        uses: actions/setup-node@v2.5.0
```

- CI/CD to ECR
깃허브 푸시 -> AWS ECR 접속, 현재 도커 파일 빌드 -> ECR로 배포
```yml
name: CI & CD

# Run this workflow every time a new tag is created
on: 
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
jobs:
  build:
    # Name the Job
    name: build and deploy image to AWS ECR
    # Set the type of machine to run on
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-northeast-2
          
      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v1
      
      - name: Set Tag Number
        id: tag-number
        run: echo ::set-output name=tag::latest
        
      - name: Check Tag Release
        env:
          RELEASE_VERSION: ${{ secrets.ECR_REGISTRY }}
        run: |
          echo $RELEASE_VERSION
          echo ${{ steps.vars.outputs.tag }}
        
      - name: Build, tag, and push image to Amazon ECR
        env:
          ECR_REGISTRY: ${{ secrets.ECR_REGISTRY }}
          ECR_REPOSITORY: ${{ secrets.ECR_REPOSITORY }}
          IMAGE_TAG: ${{ steps.tag-number.outputs.tag }}
        run: |
          docker build -t demo .
          docker tag demo:latest $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG
          docker push $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG
  deploy:
    needs: build
    name: deploy to AWS EC2
    runs-on: [ self-hosted, label-go ]
    steps:
      - name: Login to ecr
        uses: docker/login-action@v1.12.0
        with:
          registry: ${{ secrets.ECR_REGISTRY }}
          username: ${{ secrets.AWS_ACCESS_KEY_ID }}
          password: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      - name: Docker run
        run: |
          docker stop demo && docker rm demo && docker rmi ${{ secrets.ECR_REGISTRY }}/${{ secrets.ECR_REPOSITORY }}:latest
          docker run -d -p 80:3000 --name demo ${{ secrets.ECR_REGISTRY }}/${{ secrets.ECR_REPOSITORY }}:latest
          
```

- CI/CD to MyServer Docker
깃허브 푸시 -> AWS ECR 접속, 현재 도커 파일 빌드 -> ECR로 배포 -> 현재 runners가 달린 환경에서 도커 이미지 실행
