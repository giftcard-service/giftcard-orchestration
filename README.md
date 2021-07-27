# giftcard-orchestration

상품권 관리 서비스 프로젝트 관리를 위한 메인 repository.

## 기본 셋업

1. `giftcard-backend` repository를 프로젝트 최상위 경로에 클론한다.

2. `giftcard-frontend` repository를 프로젝트 최상위 경로에 클론한다.

3. `giftcard-backend`에서 `yarn`을 입력하여 패키지를 설치한다.

4. `giftcard-frontend`에서 `yarn`을 입력하여 패키지를 설치한다.

5. 배포 모드로 실행하기 위해서 프로젝트 최상위 경로의 `settings` 폴더의 .env 파일을 .template 이름만 지운 것으로 복사하여 생성한다. (e.g. .env.backed.prod)

6. 주석을 확인하며 각 .env 파일의 환경변수 내용이 key에 맞도록 value를 채운다.

## 컨테이너 실행

- `docker-compose up`과 `docker-compose down` 명령어로 컨테이너를 실행하고 중지한다.

- `docker-compose -f docker-compose.prod.yml up`과 `docker-compose -f docker-compose.prod.yml down` 명령어로 배포 모드로 실행하고 중지한다.

## 관리자 계정 생성

다음 두 가지 방법 중 하나를 택하여 관리자 계정을 만들 수 있다.

1. `pgAdmin`을 이용해 만들기

   - `서버주소:5050` 으로 접근하여 pgAdmin을 이용해 어드민 계정을 만든다. (isManager을 true로 하면 된다.)

2. API를 이용해 만들기

   1. `POST 서버주소:8000/v1/users`에 request body로 다음을 입력하여 어드민 계정을 만든다.

      ```json
      {
        "username": "관리자이름",
        "password": "관리자비밀번호",
        "isManager": true
      }
      ```

   2. 어드민 계정의 추가 생성을 막기 위해 `src/users/users.service.ts`의 다음 부분을 주석처리한다.

      ```js
      /* WARN: Comment this block to disable admin creation via API  */
      if (isManager !== undefined) {
        user.isManager = isManager;
      }
      ```
