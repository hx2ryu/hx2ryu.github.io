---
categories: git
tags: [git, github, ssh]
---

## [Git] SSH키 사용 (In Mac)

### 1. 키 생성

- 터미널 실행
- ssh 설치 경로로 이동 
  - cd ~/.ssh 입력
- 키 생성 
  - ssh-keygen 입력
  - 파일명, 패스워드, 패스워드 재입력 순차적으로 입력
    - 파일명 생략 시 **id_rsa** 로 생성
    - 그냥 엔터키 입력하면 패스워드 생략



### 2. 키 등록

- 등록하고자 하는 Githup Repository(Web)에 접속.
- Settings-Deploy keys- **add deploy key**
  - Title: 적당한 이름 입력
  - **Key: 공개키 파일 내용 입력**
    - 터미널에서 cd ~/.ssh입력
    - cat **id_rsa.pub(조금 전 생성한 공개키 파일명)** 입력
    - 내용 복사 후 다시 웹으로 이동하여 Key 입력란에 입력.
- 해당 Repository에 push도 사용할 경우 **Allow write access**에 체크.
