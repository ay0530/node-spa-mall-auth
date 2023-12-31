# API 명세서

URL : https://docs.google.com/spreadsheets/d/1Fn2_MqTjH9uQK9QHq1DYl941gy3vxyTXiWFCrCnJCcE/edit?usp=sharing

# ERD

URL : https://www.erdcloud.com/d/64Gq8tdzi2CetyoZg

# Q&A

## 1. 암호화 방식
   ### 1-1.
   단방향 암호화,
   비밀번호를 복호화하지 않고 DB에 저장된 해시값과 비교하기 때문
   ### 1-2.
   개인정보의 보안을 강화할 수 있습니다.

## 2. 인증 방식
   ### 2-1.
   주민등록번호, 비밀번호와 같이 개인정보가 담겨있을 경우 해킹의 위험성이 있습니다.
   ### 2-2.
   토큰 내에 개인정보를 담지 않습니다.

## 3. 인증과 인가
   ### 3-1.
   인증 : 사용자의 정보를 확인하는 과정(로그인 등)
   인가 : 인증된 사용자의 권한을 확인하는 과정(내 정보 수정, 등록한 상품 관리 등)
   ### 3-3.
   내 정보 조회, 상품 관리 시 권한이 있는지 확인하므로 인가에 해당됩니다.

## 4. Http Status Code
   ### 4-1.

   #### success : true

   ##### 200 : 요청 성공 시 응답 반환 (회원가입, 로그인, 상품 관리 등 에서 모두 사용)
   ##### 201 : 새로운 데이터가 성공적으로 저장되었을 때 응답 반환 (회원가입, 상품 정보 등록)

   #### success : false

   ##### 400 : 잘못된 문법 사용 시 오류 반환 (회원가입/상품 등록,수정 등에서 필수 정보들을 기입하지 않은 경우 400 에러 반환)
   ##### 401 : 인증 과정을 거치지 않았을 경우 오류 반환 (인증 미들웨어에서 로그인하지 않은 경우 401에러 반환)
   ##### 403 : 인증 과정을 거쳤으나 접근 권한이 없을 경우 오류 반환 (인증 미들웨어를 통해 인증을 했었으나 인증 유효기간이 만료되었을 때 403 반환)
   ##### 404 : 요청받은 리소스를 찾을 수 없는 경우 오류 반환 (상품 정보 [개별 조회/수정/삭제] 시 입력한 상품의 id가 DB에 존재하지 404 반환)

## 5. 리팩토링
   ### 5-1.
   DB/TABLE 생성,방식, CRUD 쿼리 방식이 모두 달랐습니다.
   ### 5-2. 
   ERD를 작성해두고 사용되는 쿼리들을 sql 파일에 기록해둔 후 기록된 정보들을 참고하여 다른 DB에 맞춰서 기능들을 수정하면 될 것 같습니다.

## 6. 서버 장애 복구
   ### 6-1. pm2 startup 명령어를 사용하여 서버 재시작 시 자동으로 pm2를 실행한다.

## 7. 개발 환경
   ### 7-1. 
   파일이 수정됐을 때 자동으로 서버를 재시작해줍니다. 서버가 자동으로 재시작되므로 테스트가 더 용이해집니다.
   ### 7-2-1 . 일반
   설명 : 프로젝트 폴더의 node_modules 폴더에 패키지가 설치되고 "dependencies" 파일에 패키지명이 기록된다.
   명령어(생략 가능) : -P, --save-prod
   ### 7-2-2. 글로벌
   설명 : 시스템(컴퓨터)폴더의 node_modules 폴더에 패키지가 설치된다.
   명령어 : -g, —global
   ### 7-2-3. 개발용
   설명 : 프로젝트 폴더의 node_modules 폴더에 패키지가 설치되고 패키지명이 "devDependencies"에 기록된다.
   명령어 : -D, —save-dev

   #### dependencies : 실제 코드에도 포함되며 앱 구동을 위해 필요한 의존성 파일들

   #### devDependencies : 실제 코드에 포함되지 않으며 개발 단계에만 필요한 의존성 파일들
