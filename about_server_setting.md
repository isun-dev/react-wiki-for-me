# 작업하면서 헷갈렸던 것.
## 리액트와 node, express를 한 프로젝트로 통합 할 수있는지?
1. proxy 개념
- 두 개 이상의 서버가 서로 통신을 주고 받을 때 그 사이에서 대리해주는, 중계해주는 것을 proxy라고 한다. 이 서버를 proxy 서버라고 한다.
2. 관련 포스팅
- https://www.bezkoder.com/integrate-react-express-same-server-port/

## node, express 설치 시 참고
1. yarn 으로 express 프로젝트 생성
- https://memostack.tistory.com/259
2. express 프로젝트 포트 변경(create-react-app 및 node 모두 3000번으로 시작)
- https://leejungyeoul.tistory.com/350
3. 개발 모드가 아니면 React에서 api 요청할 때 invalide host header 오류나는데 이때 해결 방법
- https://babysunmoon.tistory.com/entry/React-Invalid-host-header-%EC%98%A4%EB%A5%98
