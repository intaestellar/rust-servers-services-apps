# 러스트 서버, 서비스, 앱 만들기

## part1 웹서버와 웹 서비스
### 1. 왜 러스트가 웹 애플리케이션에 적합한가?
러스트는 FE, BE, SW Infra 및 그 구성 요소를 구축하는 데 모두 사용할 수 있다.

1. 타입 안정성
2. 메모리 안전성
3. 스레드 안전성

#### 무엇을 만들 것인가?
[EzyTutors라는 디지털 스토어프런트](https://github.com/user-attachments/assets/48a2e101-3155-4a59-a49e-bdfd34e9dd06)

### 2. 기본 웹서버 작성하기
3장 완료 후 읽어 보기
### 3. RESTful 웹 서비스 구축하기
Actix 소개
1. Actix를 사용해 기본적인 비동기 HTTP 서버를 구현
2. 튜터 웹 서비스를 위한 REST API를 설계하고 구현
   3. 라우트, 핸들러, 매개변수, HTTP 응답과 같은 Actix의 핵심 개념을 소개

#### Actix에서 기본적인 HTTP 서버를 생성하고 시작하는 네 단계
1. 라우트 구성
2. 핸들러 구성 (라우트에 대한 요청을 처리)
3. 웹 애플리케이션을 구축하고 라우트와 핸들러를 애플리케이션에 등록
4. 웹 애플리케이션과 연결된 HTTP 서버를 구축하고, 서버를 실행

```rust
use actix_web::{web, App, HttpResponse, HttpServer, Responder};
use std::io;

// 라우트 구성
pub fn general_routes(cfg: &mut web::ServiceConfig) {
   cfg.route("/health", web::get().to(health_check_handler));
}

// 핸들러 구성
pub async fn health_check_handler() -> impl Responder {
   HttpResponse::Ok().json("Hello. EzyTutors is alive and kicking")
}

// HTTP 서버 인스턴스화하고 실행
#[actix_rt::main]
async fn main() -> io::Result<()> {
   // app을 만들고 라우트를 구성
   let app = move || App::new().configure(general_routes);

   // HTTP 서버를 시작
   HttpServer::new(app).bind("127.0.0.1:3000")?.run().await
}
```

#### 읽고 느낀점
러스트 문법을 잘 모르기 때문에 아직 많이 어색하다. handler를 FE에서는 많이 사용했는데 BE에 나오니 이것 또한 어색하다

특히
```rust
let selected_course = app_state
        .courses
        .lock()
        .unwrap()
        .clone()
        .into_iter()
        .find(|x| x.tutor_id == tutor_id && x.course_id == Some(course_id))
        .ok_or("Course not found");
```

대충 무엇을 하는지 알겠는데 이렇게 까지 해야하는 이유는 아직 잘 모르겠다.
### 4. 데이터베이스 조작하기
### 5. 에러 핸들링하기
### 6. API의 진화와 두려움 없는 리팩터링
## part2 서버 사이드 웹 애플리케이션
### 7. 러스트를 사용한 서버 사이드 웹 애플리케이션 개요
### 8. 템플릿을 사용해 강사 등록하기
### 9. 강의 유지보수를 위한 폼 다루기
## part3 고급 주제: 비동기 러스트
### 10. 비동기 러스트 이해하기
### 11. 비동기 러스트를 사용해 P2P 노드 구현하기
### 12. 도커를 사용해 웹 서비스 배포하기