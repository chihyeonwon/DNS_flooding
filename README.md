# DNS Flooding Attack 분석 보고서
이글루코퍼레이션 원치현 DNS Flooding Attack Analyze Report

## 1. 개요
DNS Flooding Attack은 대량의 DNS 요청을 생성하여 DNS 서버의 자원을 소진시키고, 정상적인 트래픽을 방해하는 **DDoS(Distributed Denial of Service) 공격**의 한 형태입니다. 본 보고서는 DNS Flooding Attack의 원리, 유형, 영향 및 방어 방법을 분석합니다.

---

## 2. DNS Flooding Attack의 원리
DNS Flooding Attack은 공격자가 다수의 가짜 DNS 요청을 생성하여 **DNS 서버의 CPU, 메모리, 네트워크 대역폭을 소진**시키는 방식으로 이루어집니다.  
공격 유형에 따라 다음과 같이 분류할 수 있습니다.

1. **Direct Query Flooding**  
   - 공격자가 직접 대량의 DNS 요청을 보내는 방식  
   - 대상 서버의 리소스를 소모하여 응답 불가능한 상태로 만듦  

2. **Amplification Attack (증폭 공격)**  
   - 작은 요청 패킷으로 큰 응답을 유도하여 네트워크 부하를 증가  
   - 보통 **오픈 리졸버(Open Resolver)**를 이용하여 공격 수행  
   - **DNS Reflection Attack**과 조합하여 더욱 강력한 공격 수행  

3. **NXDOMAIN Attack**  
   - 존재하지 않는 도메인(예: `fake-domain-12345.com`)에 대한 대량 요청 전송  
   - DNS 서버가 응답을 생성하면서 리소스를 소모하게 됨  

---

## 3. DNS Flooding Attack의 영향
DNS Flooding Attack이 발생하면 다음과 같은 피해가 발생할 수 있습니다.

### 3.1 DNS 서버 장애
- DNS 서버가 과부하 상태가 되어 응답 속도가 느려지거나 다운됨.

### 3.2 정상 사용자 서비스 방해
- 정당한 사용자들의 DNS 요청이 처리되지 않아 웹사이트 접속 불가.

### 3.3 네트워크 부하 증가
- 대량의 트래픽이 발생하여 네트워크 대역폭이 초과될 가능성.

### 3.4 다른 서비스로의 영향 확산
- DNS 장애가 발생하면 **웹, 이메일, API 등** 여러 서비스에 영향을 미침.

---

## 4. 방어 및 대응 방법
DNS Flooding Attack을 방어하기 위해 다음과 같은 대응 방안을 적용할 수 있습니다.

### 4.1 DNS 서버 보안 설정 강화
- **Rate Limiting** 적용: 초당 요청 수 제한.
- **Response Rate Limiting(RRL)** 설정: 동일한 IP에서 오는 반복 요청 차단.
- **Recursive Query 제한**: 신뢰할 수 없는 클라이언트의 재귀 쿼리 요청 제한.

### 4.2 Anycast 네트워크 활용
- **Anycast를 사용한 트래픽 분산**으로 특정 서버가 과부하되지 않도록 설정.

### 4.3 오픈 리졸버 차단
- **DNS 서버를 오픈 리졸버로 운영하지 않도록 설정**하여 증폭 공격 방지.

### 4.4 방화벽 및 DDoS 보호 솔루션 사용
- **IP 블랙리스트 및 화이트리스트** 적용.
- Cloudflare, Akamai, AWS Shield 같은 **DDoS 방어 서비스** 활용.

### 4.5 Anomaly Detection 시스템 구축
- **비정상적인 트래픽 패턴 탐지 시스템** 구축 (예: AI 기반 분석).

---

## 5. 결론
DNS Flooding Attack은 인터넷 인프라를 마비시킬 수 있는 강력한 DDoS 공격 방식 중 하나입니다. 이를 방어하기 위해서는 **Rate Limiting, Anycast 네트워크, 오픈 리졸버 차단, 방화벽 설정 강화** 등의 다층적인 보안 대책이 필요합니다. DNS 보안이 제대로 구축되지 않으면 전체 네트워크 서비스에 심각한 영향을 미칠 수 있으므로, 주기적인 모니터링과 보안 업데이트가 필수적입니다.

---

## 6. 참고 자료
- [Cloudflare - DNS DDoS Protection](https://www.cloudflare.com/ddos/)
- [Google - Public DNS Security](https://developers.google.com/speed/public-dns/docs/security)
- [BIND 9 Rate Limiting](https://bind9.net/)


