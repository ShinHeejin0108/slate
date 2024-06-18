# 7. 해피머니

## 7.1 해피머니 잔액조회

해피머니 잔액 조회 API입니다.

잔액 조회 후 전달받는 PG거래번호(tid)는 해피머니 사용 API 호출 시 필수 파라미터로 전달하셔야 사용이 가능합니다.

**HTTP Request**

POST /kspay/webfep/api/v1/card/cancel <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=card_cancel');">테스트요청</button></code>

## 7.2 해피머니 사용 취소

해피머니 사용 취소 API입니다.

취소는 결제일 기준 6개월까지만 가능합니다.

**HTTP Request**

POST /kspay/webfep/api/v1/card/cancel <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=card_cancel');">테스트요청</button></code>


## 7.3 해피머니 사용

해피머니 사용 API입니다.

잔액 조회 후 사용이 가능하며 결제 금액보다 잔액이 크거나 같은지 확인 후 API 호출하시기 바랍니다.

결제 요청 시 잔액조회를 통해 전달받은 PG거래번호를 올바르게 넣어야 결제가 가능합니다.

**HTTP Request**

POST /kspay/webfep/api/v1/card/cancel <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=card_cancel');">테스트요청</button></code>
