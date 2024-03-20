JWT 기초
- Json Web Token = JWT
- 편지 역할
- Header, Payload, Signature 이것들을 base64로 인코딩
- 사용처: **Authentication**, Information Exchange, Authorization, Single Sign-On, Server-to Server communication
- 쿠키 기반 인증 vs JWT 기반 인증
- DB에 부담을 덜어준다. DB에 덜 접속해도 되니 빠르다. 
- 서버에 Signature가 존재하고 클라이언트가 서버에 인증을 요청하면 존재하는 Signature와 수신된 header,payload를 사용해 생성된 Signature을 비교함!


 - Header: JWT의 header에는 두 가지 정보가 포함됩니다. 첫째, 토큰의 타입을 나타내는 "typ" (예: "JWT")과 둘째, 사용된 해싱 알고리즘을 나타내는 "alg" (예: "HS256" 또는 "RS256")이 포함됩니다.
- Payload: JWT의 payload에는 클레임(claim)이 포함됩니다. 클레임은 토큰에 담길 정보들을 말하며, 세 가지 타입으로 나뉩니다: registered, public, private 클레임이며, 이들은 토큰에 대한 메타데이터, 사용자 정보 등을 포함합니다.
- Signature: 서명은 header와 payload를 합친 후, 이를 비밀 키(secret key)나 개인 키(private key)를 사용하여 해싱한 값입니다. 이 서명은 토큰이 변경되지 않았음을 확인하고, 발행자가 인증되었음을 보장합니다.
- 서버에는 JWT의 header에 알고리즘 정보가 포함되어 있고, 이 알고리즘에 따라 서명이 생성되어 있습니다. 이 서명을 사용하여 토큰의 무결성을 확인할 수 있습니다
## Reference
- https://youtu.be/36lpDzQzVXs?si=fqFpB8ZqEcRCINzR