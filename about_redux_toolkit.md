## prepareHeaders
- Allows you to inject headers on every request. You can specify headers at the endpoint level, but you'll typically want to set common headers like authorization here. As a convenience mechanism, the second argument allows you to use getState to access your redux store in the event you store information you'll need there such as an auth token. Additionally, it provides access to extra, endpoint, type, and forced to unlock more granular conditional behaviors.
- 모든 요청에 헤더를 주입할 수 있습니다. 끝점 수준에서 헤더를 지정할 수 있지만 일반적으로 여기서 인증과 같은 공통 헤더를 설정할 수 있습니다. 두 번째 인수를 사용하면 getState를 사용하여 인증 토큰과 같은 필요한 정보를 저장할 때 중복 제거 저장소에 액세스할 수 있습니다. 또한 추가, 끝점, 유형 및 보다 세분화된 조건부 동작에 대한 액세스를 제공합니다.