### APIGATEWAY 통합 전략

목표 : 기존 Spring-cloud apigateway 적용 및 수정 최소화 , Devops Resource 변경 안하고 바로 연결

### 기존 yml 작성 : 계획 그대로

> user deploy-service.yml
apigateway deploy-service.yml
> 

나머지 msa도 그대로

### ingress 구성 : apigatewayTargetGrouping

> ingress -> 8089
/api
/open-api
> 

### 예시

case : 외부 유저 igw - (생략) - alb - ingress -> 어디 포트로 보내냐?

> 원래:
ingress에서 8081 ~ 8088에 각자 url 기반 routing
> 

> 지금:
모든 api, openapi 요청- apigateway(8089) -> 8081 - 8088 url 기반 routing
> 

### Traffic Path (3 step)

> client →igw→ alb ->(생략) → (frontend Trigger) → API Caller

>→ ingress  -> apigateway(springcloud)

>→ **k8s discovery, Route by lb : k8s - service - name  → SVC Dept**
