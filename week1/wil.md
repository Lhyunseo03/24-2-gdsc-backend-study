# 1주차

추가 일시: 2024년 9월 11일 오후 6:00
강의: 초급 백엔드 스터디

### 웹

네이버는 큰 컴퓨터이다 (서버)

클라이언트 → 서버 : 데이터에 관한 요청

서버→ 클라이언트 : 요청대로 수행하고 응답 전송

요청과 응답을 보내는 규칙 → 프로토콜

웹에서 사용하는 프로토콜 → HTTP

예시)

(요청) GET [http://www.naver.com](http://www.naver.com/) → 네이버 메인화면 데이터 주세요
(응답)<html>naver source code</html> → 여기 네이버 html 코드요

### <프로토콜을 통해 요청할 때> 필요한 것 두 가지

1. HTTP Method - 데이터를 다루는 방법(어떻게)
    
    POST(생성): 중복으로 계속 생성
    
    PUT(수정): 중복 안됨 리소스의 모든 것을 업데이트 
    
    PATCH(수정): 일부분 뜯어 고침 게임 패치 처럼 리소스의 일부만 업데이트
    
    3개를 구분해야 한다
    
    나머지: GET(조회), DELETE(삭제)
    
2. URL - 다룰 데이터의 위치(무엇을)
    
    구조: 프로토콜://서버주소/서버내데이터위치
    ex)[http://www.example.com/user/{user_id}/nickname](http://www.example.com/user/%7Buser_id%7D/nickname)
    
    이 뒤에 Query string을 붙이기도 함
    
    -서버에 추가적으로 정보(조건) 전달
    
    -물음표 쓰고 조건 붙이고 
    
    https: 보안 강화
    

### HTTP 데이터의 구조(요청이든 응답이든 왔다갔다하는 데이터)

- HTTP 헤더: 통신에 대한 정보(언제 보냈는지, 누가 보내는지, HTTP method 종류, 요청 경로 등)
- HTTP 바디: 데이터 (json 형식)

### 상태 코드

처리 결과 성공/실패했을 경우 알려줘야 됨(응답)

규칙: 어떻게 보낼지 정해놓음 → 상태 코드

상태 코드는 헤더에 포함됨

잘 처리했다면 200 ← 이건 강조용? ok

이상해서 처리 못함 → 400 bad request

데이터 없음 → 404 not found

서버 에러 → 500 intrnal server error

ex) 요청: 네이버 메인화면 주세요(메소드+URL) → 응답: 200OK + 네이버 html 소스코드

### 프론트엔드 ↔ 백엔드

자주 안변하는 콘텐츠가 프론트엔드

자주 변하는건 프→백 요청해서 백엔드가 DB의 컨텐츠 데이터를 프론트에게 응답

→ 클라이언트 : 프론트 / 서버 : 백엔드

주로 json 형태의 데이터를 주고받음

## API(Application Programming Interface)

### API란?

프론트와 백엔드는 각각 웹에서 동작하며 HTTP(프로토콜)를 사용하여 통신함

HTTP는 데이터를 주고받는 단순한 규칙

HTTP 안에 직접 정의된 구체적인 통신 방법이 API 이다. 

<어플리케이션의 사용 설명서>

백엔드 API: 프론트→백으로 요청 보낼때 어떤 메소드와 url 을 사용해야하는지 정의

REST API 쫌 자잘한 규칙들

## 프로젝트- 투두메이트 API 서버 클론 코딩

### API 명세 작성하기 - 규칙 정하기?

- HTTP METHOD 정의
- URL 정의
    - 공통적인 서버 정보(프로토콜, 서버 주소)를 빼고 path 만 정의
    - 점점 구체화 되도록 작성
    - 로그인같은 간단한 동사 아니면 명사를 씀
- request body, request header, response body, status code 정의는 나중에

<세부 기능>
• 유저 회원가입 / 로그인
• 로그인한 유저의 할 일 생성 / 조회 / 수정 / 삭제
• 로그인한 유저의 할 일 체크 / 체크 해제
• 친구 추가 / 친구 조회 / 친구 삭제
• 특정 친구의 할 일 조회

- /member/{member_id}/nickname
→ member 그룹 안에서,
{member_id} 를 가진 member의,
nickname 데이터

| 세부 기능 | HTTP 메소드 | URL |
| --- | --- | --- |
| 유저 회원가입 | POST | /register |
| 유저 로그인 | POST | /login |
| 유저 로그아웃 | POST | /logout |
| 할 일 생성 | POST | /todo |
| 할 일 전체 조회 | GET | /todo/list |
| 할 일 수정 | PATCH | /todo/{todo_id} |
| 할 일 삭제 | DELETE | /todo/{todo_id} |
| 할 일 체크 | POST | /todo/{todo_id}/check |
| 할 일 체크해제 | POST | /todo/{todo_id}/uncheck |
| 친구 추가 | POST | /member/{member_id} |
| 친구 조회 | GET | /member/{member_id} |
| 친구 삭제 | DELETE | /friend/{friend_id} |
| 특정 친구의 할 일 조회 | GET | /member/{member_id}/todo |
| 좋아요 | POST | /like |
| 프로필 편집 | PATCH | /member/{member_id}/profile |

### [localhost:8080](http://localhost:8080) 에러화면 첨부

![스크린샷 2024-09-22 183657.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ba1a5998-ec4e-4213-a110-4fadaf91e17c/5e668f6a-747f-4365-81b9-e4094627fdbf/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2024-09-22_183657.png)