# 7. 해피머니 API

## 7.1 해피머니 잔액조회

해피머니 잔액 조회 API입니다.

잔액 조회 후 전달받는 PG거래번호(tid)는 해피머니 사용 API 호출 시 필수 파라미터로 전달하셔야 사용이 가능합니다.

**HTTP Request**

POST /kspay/webfep/api/v1/happymoney/balance <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=happymoney_balance');">테스트요청</button></code>

### 요청항목

> 해피머니 잔액 조회 요청 예시

```예시
{
    "mid": "2999199999",
    "payload": "",
    "happyMoneyUserId": "kspay",
    "happyMoneyUserPw": "0000"
}
```

Name | Size | Description
--------- |---- | ------------------
mid*  | 10 |**상점아이디**<br>- 계약 완료 후 사업부를 통해 전달받은 상점아이디
payload  | * | **가맹점데이터**<br>- API 응답에 돌려받을 가맹점의 데이터입니다.
happyMoneyUserId*  | 20  | **해피머니 사용자 아이디**
happyMoneyUserPw*  | 50 | **해피머니 사용자 패스워드**

### 응답항목(Body > data)
> 신용카드 결제 취소 응답 예시

```예시
# 성공응답
{
    "aid": "WF2HBSI00000000000002880",
    "code":"A0200",
    "message":"Success",
    "data": {
        "payload": "",
        "tid": "",
        "tradeDateTime": "20240624083737",
        "respCode": "0000",
        "respMessage": "",
        "happyMoneyBalance": ""
    }}

# 실패응답
{
    "aid": "WF2HBSI00000000000002880",
    "code": "A0201",
    "message": "Fail",
    "data": {
        "payload": "",
        "tid": "",
        "tradeDateTime": "20240624083737",
        "respCode": "30002",
        "respMessage": "가맹점ID 없음",
        "happyMoneyBalance": ""
    }}
```

Name | Size | Description
--------- | ---- | -----------------------
tid  | 12  | PG거래번호
tradeDateTime | 14 | 거래일시(yyyyMMddHHmmss)
cancelAmount  | 9  | 취소된금액
respCode  | 4  | 응답코드
respMessage  | 40  | 응답메시지
payload  | *  | 가맹점데이터
happyMoneyBalance  | 9  | 해피머니 잔액

## 7.2 해피머니 사용 취소

해피머니 사용 취소 API입니다.

취소는 결제일 기준 6개월까지만 가능합니다.

**HTTP Request**

POST /kspay/webfep/api/v1/happymoney/cancel <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=happymoney_cancel');">테스트요청</button></code>

### 요청항목

> 해피머니 사용 취소 요청 예시

```예시
{
    "mid": "2999199999",
    "payload": "",
    "orgTradeKeyType": "TID",
    "orgTradeKey": "G89449000001",
    "orgTradeDate": ""
}
```
Name | Size | Description
--------- |---- | ------------------
mid*  | 10 |**상점아이디**<br>- 계약 완료 후 사업부를 통해 전달받은 상점아이디
payload  | * | **가맹점데이터**<br>- API 응답에 돌려받을 가맹점의 데이터입니다.
orgTradeKeyType*  | 50 |**거래키구분<br>- TID : 결제 응답으로 부여받은 tid 값<br>- ORDER_NUMB : 결제 요청 시 생성한 가맹점 주문번호
orgTradeKey*  | 50 |**원거래 키<br>- 원거래 구분에 해당하는 TID 혹은 ORDER_NUMB 값
orgTradeDate  | 8 |**원거래일자<br>- 주문번호 취소시 설정필요(yyyyMMdd)

### 응답항목(Body > data)
> 카드 인증 응답 예시

```예시
# 성공응답
{
    "aid": "WFVHCSI00000000003100202",
    "code":"A0200",
    "message":"Success",
    "data": {
        "payload": "",
        "tid": "G89449000001",
        "tradeDateTime": "20240624084540",
        "respCode": "0000",
        "respMessage": "",
        "happyMoneyApprovalNumb": ""
    }}

# 실패응답
{
    "aid": "WFVHCSI00000000003100202",
    "code": "A0201",
    "message": "Fail",
    "data": {
        "payload": "",
        "tid": "G89449000001",
        "tradeDateTime": "20240624084540",
        "respCode": "50006",
        "respMessage": "결제내역 없음",
        "happyMoneyApprovalNumb": ""
    }}
```
Name | Size | Description
--------- | ---- | -----------------------
tid  | 12  | PG거래번호
respCode  | 4  | 응답코드
respMessage  | 40  | 응답메시지
payload  | *  | 가맹점데이터
happyMoneyApprovalNumb | 12 | 해피머니 승인번호

## 7.3 해피머니 사용

해피머니 사용 API입니다.

잔액 조회 후 사용이 가능하며 결제 금액보다 잔액이 크거나 같은지 확인 후 API 호출하시기 바랍니다.

결제 요청 시 잔액조회를 통해 전달받은 PG거래번호를 올바르게 넣어야 결제가 가능합니다.

**HTTP Request**

POST /kspay/webfep/api/v1/happymoney/pay <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=happymoney_pay');">테스트요청</button></code>

### 요청항목

> 해피머니 사용 요청 예시

```예시
{
    "mid": "2999199999",
    "orderNumb": "kspay_1234",
    "userName": "홍길동",
    "userEmail": "",
    "productType": "REAL",
    "productName": "핑크테디",
    "totalAmount": "1004",
    "taxFreeAmount": "0",
    "payload": "",
    "happyMoneyUserId": "kspay",
    "happyMoneyPayKey": "G89449000001"
}
```

Name | Size | Description
--------- |---- | ------------------
mid*  | 10 |**상점아이디**<br>- 계약 완료 후 사업부를 통해 전달받은 상점아이디
orderNumb*  | 50 |**가맹점 주문번호**
userName*  | 50 |**주문자명**
userEmail  | 50 |**주문자이메일**
productType*  | 10 |**상품구분**<br>- REAL : 실물상품, DIGITAL : 디지털컨텐츠
productName*  | 50 |**상품명**
totalAmount*  | 9 |**총금액**
taxFreeAmount*  | 9 |**면세금액**<br>- 면세금액이 없으면 총금액 전체 과세처리
payload  | * | **가맹점데이터**<br>- API 응답에 돌려받을 가맹점의 데이터입니다.
happyMoneyUserId*  | 20 |**해피머니 사용자 아이디**
happyMoneyPayKey*  | 12 |**해피머니 결제키**<br>- 해피머니 잔액조회를 통해 부여받은 PG거래번호(tid)를 사용합니다.

```예시
# 성공응답
{
    "aid": "WF2HPSI00000000000002893",
    "code":"A0200",
    "message":"Success",
    "data": {
        "payload": "",
        "tid": "",
        "tradeDateTime": "20240624084437",
        "respCode": "0000",
        "respMessage": "",
        "happyMoneyApprovalNumb": ""
  }}

# 실패응답
{
    "aid": "WF2HPSI00000000000002893",
    "code": "A0201",
    "message": "Fail",
    "data": {
        "payload": "",
        "tid": "",
        "tradeDateTime": "20240624084437",
        "respCode": "30002",
        "respMessage": "가맹점ID 없음",
        "happyMoneyApprovalNumb": ""
    }}
```

Name | Size | Description
--------- | ---- | -----------------------
tid  | 12  | PG거래번호
tradeDateTime | 14 | 거래일시(yyyyMMddHHmmss)
respCode  | 4  | 응답코드
respMessage  | 40  | 응답메시지
payload  | *  | 가맹점데이터
happyMoneyApprovalNumb  | 20  | 해피머니 승인번호
