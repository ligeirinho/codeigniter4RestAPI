# Users Restful API
JWT 토큰기반 인증방식을 사용한 회원관리 Restful API 구현

## Stack
- PHP 7.3
- MySQL 5.7
- Codeigniter4

## Step
1. users.sql 실행합니다. (초기 관리자 셋팅을 위해 insert구문까지 등록)
2. 로그인을 통해 사용자 토큰을 발급받습니다. (토큰 만료 시간: 발급 시간 +30분)
3. 발급된 토큰을 Headers의 Authorization에 등록 후 Users API를 호출합니다.
<img src="./readme_asset/post_login.PNG" style="float:left"/>
<br>

## Login
**초기 관리자 이메일: admin<span></span>@admin.com**

**초기 관리자 패스워드: Admin1234!@**

>회원 로그인(인증)
```
[POST] /login  회원 로그인

Request
Parameters
    email     string (requrid) 사용자 이메일
    password  string (requrid) 사용자 암호
Headers
     Context-Type: application/json
     
Response 200
Header
    Context-Type: application/json
Body
{
    "messages": "login success",
    "email: "test@abc.com",
    "access_token" : "token_info"
}

```

## Users
**로그인 인증 성공 후 access_token을 발급받아 사용**

>여러 회원 목록 조회
```
[GET] /users

Request
Parameters
    name   string (optional) 사용자 이름으로 조회 (Example: 관리자)   
    email  string (optional) 사용자 이메일로 조회 (Example: admin@admin.com)
    limit  int    (optional) 출력 갯수
    offset int    (optional) 출력 시작 row
Headers
     Context-Type: application/json
     Authorization: Bearer {access_token}
```
>단일 회원 상세 정보 조회
```
[GET] /users/{id}  

Request
Parameters
    id int (requrid) 사용자 코드
Headers
     Context-Type: application/json
     Authorization: Bearer {access_token}
```
>회원 가입
```
[POST] /users 

Request
Parameters
     name      string (required) 사용자 이름　　 [한글, 영문 대소문자만 허용]
     nickname  string (required) 사용자 별　　　 [영문 소문자만 허용]
     password  string (required) 사용자 비밀번호 [영문 대문자, 영문 소문자, 특수 문자, 숫자 각 1개 이상씩 포함]
     phone     string (required) 사용자 전화번호 [숫자]
     email     string (required) 사용자 이메일　 [이메일 형식]
     gender    string (optional) 사용자 성별　　 [M or F]
Headers
     Context-Type: application/json
     Authorization: Bearer {access_token}
```
