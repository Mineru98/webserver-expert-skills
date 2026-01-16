# webserver-expert-skills

웹 서버(nginx, Apache, IIS) 관리를 위한 Claude Code 전문 에이전트 플러그인

## 설치

### Claude Code에서 플러그인 설치

1. Claude Code CLI를 실행합니다
2. 다음 명령어로 플러그인을 설치합니다:

```bash
claude plugin install https://github.com/Mineru98/webserver-expert-skills.git
```

또는

```bash
claude plugin install webserver-expert
```

3. 설치 후 사용 가능한 에이전트와 스킬을 확인합니다:

```bash
claude plugin list
```

## 주요 기능

### 전문 에이전트

3가지 웹 서버 전문 에이전트가 포함되어 있습니다:

- **nginx-expert**: nginx 프록시 서버 구성 및 운영 전문가
- **apache-expert**: Apache HTTP 서버 관리 전문가
- **iis-expert**: Windows IIS 서버 관리 전문가

### Web Server Manager 스킬

자연어로 웹 서버 관리 작업을 요청할 수 있습니다:

- **SSL/TLS 인증서 관리**: Let's Encrypt, 상용 인증서 설정 및 갱신
- **로드 밸런싱**: upstream 서버 구성, 알고리즘 선택, health check
- **서브도메인 관리**: 가상 호스트, 와일드카드 도메인 설정
- **보안 강화**: 보안 헤더, rate limiting, IP 필터링
- **성능 최적화**: 캐싱, 압축, worker 프로세스 튜닝
- **HTTPS 리다이렉트**: HTTP → HTTPS 자동 전환
- **HTTP/2 설정**: HTTP/2 프로토콜 활성화
- **백업/복원**: 설정 파일 백업 및 복원
- **트러블슈팅**: 502/504 에러, SSL 문제, 성능 이슈 진단

## 워크플로우

### 1. 자연어로 요청하기

웹 서버 관리 작업을 자연어로 요청합니다:

```
"example.com에 Let's Encrypt SSL 인증서를 설정해줘"

"nginx에 로드 밸런서를 설정해줘. 백엔드는 backend1:8080, backend2:8080이야"

"Apache 보안을 강화하고 HSTS 헤더를 추가해줘"

"nginx에서 502 에러가 발생해. upstream timeout 메시지가 보여"
```

### 2. 자동 라우팅

플러그인이 자동으로 요청을 분석하여 적절한 전문 에이전트로 라우팅합니다:

- 웹 서버 타입 감지 (nginx/Apache/IIS)
- 작업 카테고리 분류 (ssl/loadbalancer/security 등)
- 관련 컨텍스트 추출 (도메인, 서버 주소, 에러 메시지 등)

### 3. 전문가 응답

해당 웹 서버 전문 에이전트가 프로덕션 환경에 적합한 설정과 가이드를 제공합니다:

- 검증된 설정 파일 템플릿
- 단계별 실행 가이드
- 문법 검증 명령어
- 주의사항 및 베스트 프랙티스

## 사용 예시

### SSL 인증서 설정

```
User: "nginx에 example.com SSL을 설정해줘. Let's Encrypt를 사용하고 싶어"

Agent: nginx-expert가 다음을 제공합니다:
- Certbot 설치 및 실행 명령어
- nginx SSL 설정 블록
- 자동 갱신 cron 설정
- 검증 및 reload 절차
```

### 로드 밸런싱 구성

```
User: "Apache에 로드 밸런서를 설정해줘. 백엔드는 10.0.1.1:8080, 10.0.1.2:8080이고 least_conn 알고리즘을 쓰고 싶어"

Agent: apache-expert가 다음을 제공합니다:
- mod_proxy_balancer 활성화
- BalancerMember 설정
- lbmethod=bybusyness 설정 (least_conn)
- 헬스 체크 설정
```

### 트러블슈팅

```
User: "nginx에서 502 bad gateway 에러가 자주 발생해. upstream timeout 메시지가 error.log에 보여"

Agent: nginx-expert가 다음을 제공합니다:
- upstream 서버 상태 확인 방법
- proxy_read_timeout 조정
- upstream 서버 health check 설정
- 백엔드 성능 최적화 권장사항
```

## 에이전트 직접 호출

스킬 대신 에이전트를 직접 호출할 수도 있습니다:

```
# Task tool을 사용하여 직접 호출
subagent_type: "webserver-expert:nginx-expert:AGENT"
prompt: "SSL 인증서 자동 갱신을 설정해줘"
```

## 요구사항

- Claude Code CLI 설치
- 관리하려는 웹 서버(nginx/Apache/IIS)가 설치된 환경
- (선택) Let's Encrypt 사용 시 도메인 DNS 설정

## 라이선스

GPL-3.0

## 기여

이슈 및 PR은 [GitHub](https://github.com/Mineru98/webserver-expert-skills)에서 환영합니다.

## 작성자

- **Mineru** - [mineru@usefullabs.co.kr](mailto:mineru@usefullabs.co.kr)
