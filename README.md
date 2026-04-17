# hang9-hub

항(구)-HUB는 컴퓨터공학과 학생들을 위한 공부자료 공유, 판매, 후원 웹 애플리케이션입니다. 사용자는 강의 자료, 설계 자료, 학습 노하우를 게시물로 등록하고, 필요한 자료를 구매하거나 후원할 수 있습니다.

## 기술 스택

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![EJS](https://img.shields.io/badge/EJS-B4CA65?style=for-the-badge&logo=ejs&logoColor=111111)
<br>

![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=111111)
![npm](https://img.shields.io/badge/npm-CB3837?style=for-the-badge&logo=npm&logoColor=white)
<br>

![Multer](https://img.shields.io/badge/Multer-FFB020?style=for-the-badge&logoColor=111111)

## 주요 기능

- 홈 화면, 로그인, 회원가입 화면
- 게시판 목록, 게시물 상세, 작성, 수정, 삭제
- 게시물 이미지 업로드
- 카테고리와 형식 기반 게시물 필터링
- 조회수, 추천수, 다운로드수 증가
- 장바구니 추가, 삭제, 조회
- 게시물 구매 및 장바구니 결제
- 세션 기반 로그인 상태 관리
- 관리자/회원/작성자 권한 검사

## 실행 환경

다음 프로그램이 필요합니다.

- Node.js
- npm
- MySQL 8.x

현재 DB 접속 설정은 [database/config.json](database/config.json)에 있습니다.

```json
{
  "host": "localhost",
  "port": 3306,
  "user": "root",
  "password": "1234",
  "database": "sedb3"
}
```

로컬 MySQL 설정이 다르면 `database/config.json`의 `user`, `password`, `database` 값을 환경에 맞게 수정해야 합니다.

## 설치

```powershell
cd C:\Users\User\repositories\hang9-hub
npm install
```

## 데이터베이스 초기화

초기화 스크립트는 `sedb3` 데이터베이스에 접속한 뒤 테이블과 기본 데이터를 생성합니다. 데이터베이스가 아직 없다면 먼저 생성합니다.

```powershell
mysql -uroot -p1234 -e "CREATE DATABASE IF NOT EXISTS sedb3;"
node database\init.js
```

초기화가 성공하면 다음 메시지가 출력됩니다.

```text
Success to initialize database
```

기본 계정은 [database/sqls/setup_default.sql](database/sqls/setup_default.sql)에 정의되어 있습니다.

| 로그인 ID | 비밀번호 | 권한        |
| --------- | -------- | ----------- |
| `admin`   | `admin`  | 관리자      |
| `tester`  | `tester` | 일반 사용자 |

## 실행

기본 포트는 `80`입니다. 일반 사용자 권한에서는 포트 80 실행이 실패할 수 있으므로 개발 중에는 `PORT=3000`을 지정하는 것을 권장합니다.

```powershell
$env:PORT="3000"
npm start
```

브라우저에서 다음 주소로 접속합니다.

```text
http://127.0.0.1:3000/
```

서버를 종료하려면 실행 중인 PowerShell에서 `Ctrl + C`를 누릅니다.

## 프로젝트 구조

```text
hang9-hub/
├─ app.js
├─ bin/
│  └─ www
├─ controllers/
├─ database/
│  ├─ config.json
│  ├─ init.js
│  └─ sqls/
├─ middlewares/
├─ models/
├─ public/
│  ├─ images/
│  ├─ javascripts/
│  ├─ stylesheets/
│  └─ uploads/
├─ routes/
├─ views/
├─ package.json
└─ package-lock.json
```

## 개발 참고

- 서버 진입점은 [app.js](app.js)입니다.
- 실제 HTTP 서버 실행 파일은 [bin/www](bin/www)입니다.
- DB 초기화 로직은 [database/init.js](database/init.js)입니다.
- 라우터는 [routes](routes)에 있습니다.
- 화면 템플릿은 [views](views)에 있습니다.
- 정적 파일은 [public](public)에 있습니다.
