# 7. 해피머니

## 7.1 해피머니 잔액조회

해피머니 잔액 조회 API입니다.

잔액 조회 후 전달받는 PG거래번호(tid)는 해피머니 사용 API 호출 시 필수 파라미터로 전달하셔야 사용이 가능합니다.

**HTTP Request**

POST /kspay/webfep/api/v1/happymoney/balance <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=happymoney_balance');">테스트요청</button></code>

### 요청항목

> 해피머니 잔액 조회 요청 예시

```예시
{
    "mid": "상점아이디",
    "payload": "",
    "happyMoneyUserId": "해피머니 사용자 아이디",
    "happyMoneyUserPw": "해피머니 사용자 패스워드"
}
```

Name | Size | Description
--------- |---- | ------------------
mid*  | 10 |**상점아이디**<br>- 계약 완료 후 사업부를 통해 전달받은 상점아이디
payload  | * | **가맹점데이터**<br>- API 응답에 돌려받을 가맹점의 데이터입니다.
happyMoneyUserId *  | 10  | **해피머니 사용자 아이디**
happyMoneyUserPw *  | 10 | **해피머니 사용자 패스워드**

### 응답항목(Body > data)
> 신용카드 결제 취소 응답 예시

```예시
# 성공응답
{
  "aid":"WFVCCSE00000000000054321",
  "code":"A0200",
  "message":"Success",
  "data": {
    "payload": "KST20240604S031",
	"tid":"189189008016",
    "tradeDateTime":"20240604120147",
    "cancelAmount":"50004",
    "respCode":"0000",
    "respMessage":"승인취소완료/매입취소요청",
    "issuerCardType":"HYUNDAI",
    "issuerCardName":"현대카드",
    "purchaseCardType":"HYUNDAI",
    "purchaseCardName":"현대카드",
    "approvalNumb":"00876543",
    "cardNumb":"40176201XXXX825X",
    "expiryDate":"",
    "installMonth":"03"
}}

# 실패응답
{
  "aid":"WFVCCSE00000000000054320",
  "code":"A0201",
  "message":"Fail",
  "data": {
    "payload": "KST20240604S027",
	"tid":"Lbd124090990",
    "tradeDateTime":"20240604102151",
    "cancelAmount":"",
    "respCode":"7003",
    "respMessage":"취소거절기간경과/Tel:1544-6030",
    "issuerCardType":"UNDEFINED",
    "issuerCardName":"미등록카드사",
    "purchaseCardType":"UNDEFINED",
    "purchaseCardName":"미등록카드사",
    "approvalNumb":"7003",
    "cardNumb":"",
    "expiryDate":"",
    "installMonth":""
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
happyMoneyBalance  | 20  | 해피머니 잔액

## 7.2 해피머니 사용 취소

해피머니 사용 취소 API입니다.

취소는 결제일 기준 6개월까지만 가능합니다.

**HTTP Request**

POST /kspay/webfep/api/v1/happymoney/cancel <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=happymoney_cancel');">테스트요청</button></code>

### 요청항목

> 해피머니 사용 취소 요청 예시

```예시
{
    "mid": "상점아이디",
    "payload": "가맹점데이터",
    "orgTradeKeyType": "거래키구분",
    "orgTradeKey": "원거래 키",
    "orgTradeDate": "원거래일자"
}
```
Name | Size | Description
--------- |---- | ------------------
mid*  | 10 |**상점아이디**<br>- 계약 완료 후 사업부를 통해 전달받은 상점아이디
payload  | * | **가맹점데이터**<br>- API 응답에 돌려받을 가맹점의 데이터입니다.
orgTradeKeyType*  | 50 |**거래키구분<br>- TID : 결제 응답으로 부여받은 tid 값<br>- ORDER_NUMB : 결제 요청 시 생성한 가맹점 주문번호
orgTradeKey*  | 50 |**원거래 키
orgTradeDate*  | 50 |**원거래일자

### 응답항목(Body > data)
> 카드 인증 응답 예시

```예시
# 성공응답
{
  "aid": "API 요청 고유값",
  "code": "API 응답 코드",
  "message": "API 응답 메시지",
  "data": {
    "tid": "PG거래번호",
    "tradeDateTime": "거래일시",
    "respCode": "승인코드",
    "respMessage": "응답메시지",
    "payload": "가맹점 데이터",
    "happyMoneyApprovalNumb": "해피머니 승인번호"
  }
}

# 실패응답
{
  "aid": "API 요청 고유값",
  "code": "API 응답 코드",
  "message": "API 응답 메시지",
  "data": {
    "tid": "PG거래번호",
    "tradeDateTime": "거래일시",
    "respCode": "승인코드",
    "respMessage": "응답메시지",
    "payload": "가맹점 데이터",
    "happyMoneyApprovalNumb": "해피머니 승인번호"
  }
}
```
Name | Size | Description
--------- | ---- | -----------------------
tid  | 12  | PG거래번호
respCode  | 4  | 응답코드
respMessage  | 40  | 응답메시지
payload  | *  | 가맹점데이터
happyMoneyApprovalNumb | 14 | 해피머니 승인번호

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
    "mid": "required",
    "orderNumb": "required",
    "userName": "required",
    "userEmail": "",
    "productType": "required",
    "productName": "required",
    "totalAmount": "required",
    "taxFreeAmount": "required",
    "payload": "",
    "happyMoneyUserId": "required",
    "happyMoneyPayKey": "required"
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
taxFreeAmount  | 9 |**면세금액**<br>- 면세금액이 없으면 총금액 전체 과세처리
payload  | * | **가맹점데이터**<br>- API 응답에 돌려받을 가맹점의 데이터입니다.
happyMoneyUserId*  | 20 |**해피머니 사용자 아이디**
happyMoneyPayKey*  | 4 |**해피머니 결제키**<br>- 해피머니 잔액조회를 통해 부여받은 PG거래번호(tid)를 사용합니다.

```예시
# 성공응답
{
  "aid": "API 요청 고유값",
  "code": "API 응답 코드",
  "message": "API 응답 메시지",
  "data": {
    "tid": "PG거래번호",
    "tradeDateTime": "거래일시",
    "respCode": "승인코드",
    "respMessage": "응답메시지",
    "payload": "가맹점 데이터",
    "happyMoneyApprovalNumb": "해피머니 승인번호"
  }
}

# 실패응답
{
  "aid": "API 요청 고유값",
  "code": "API 응답 코드",
  "message": "API 응답 메시지",
  "data": {
    "tid": "PG거래번호",
    "tradeDateTime": "거래일시",
    "respCode": "승인코드",
    "respMessage": "응답메시지",
    "payload": "가맹점 데이터",
    "happyMoneyApprovalNumb": "해피머니 승인번호"
  }
}
```

Name | Size | Description
--------- | ---- | -----------------------
tid  | 12  | PG거래번호
tradeDateTime | 14 | 거래일시(yyyyMMddHHmmss)
respCode  | 4  | 응답코드
respMessage  | 40  | 응답메시지
payload  | *  | 가맹점데이터
happyMoneyApprovalNumb  | 20  | 해피머니 승인번호
