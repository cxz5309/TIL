# JWT(Json Web Token)
- 전자 서명 된 URL-safe (URL로 이용할 수있는 문자 만 구성된)의 JSON이다.
- 전자 서명은 JSON 의 변조를 체크 할 수 있게되어 있다.
- JWT는 속성 정보 (Claim)를 JSON 데이터 구조로 표현한 토큰으로 RFC7519 표준이다.
- JWT는 서버와 클라이언트 간 정보를 주고 받을 때 Http 리퀘스트 헤더에 JSON 토큰을 넣은 후 서버는 별도의 인증 과정없이 헤더에 포함되어 있는 JWT 정보를 통해 인증한다.
- 이때 사용되는 JSON 데이터는 URL-Safe 하도록 URL에 포함할 수 있는 문자만으로 만든다.
- JWT는 HMAC 알고리즘을 사용하여 비밀키 또는 RSA를 이용한 Public Key/ Private Key 쌍으로 서명할 수 있다.