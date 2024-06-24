# 영구 가상계좌 발급 API

## 영구 가상계좌 발급 API

영구성 가상계좌 발급 요청에 대한 API입니다.

**HTTP Request**

POST /kspay/webfep/api/v1/vaccount/permanent <code><button type="button" onclick="javascript:window.open('https://pgdev.ksnet.co.kr/kspay/webfep//api/test/x.jsp?api=vaccount_permanent');">테스트요청</button></code>

### 요청항목

> 영구성 가상계좌 발급 요청 예시

```예시
{
    "mid": "2999199994",
    "orderNumb": "carrot12212",
    "orderName": "김토끼",
    "goodName": "당근12kg",
    "totalAmount": "1004",
    "payload": "",
    "bankType": "NONGHYUP",
    "virtAccountType": "2",
    "escrowType": "",
    "closeDateTime": "20240624100000",
    "virtAccountNumb": "10185164017326"
}
```

Name | Size | Description
--------- |---- | ------------------
mid*  | 10 |**상점아이디**<br>- 계약 완료 후 사업부를 통해 전달받은 상점아이디
orderNumb*  | 50 |**가맹점 주문번호**
userName*  | 50 |**주문자명**
productName*  | 50 |**상품명**
totalAmount*  | 9 |**결제금액**
payload  | * | **가맹점데이터**<br>- API 응답에 돌려받을 가맹점의 데이터입니다.
bankType*  | *  | **은행타입**<br>- 은행타입표를 참고하셔서 가상계좌 발급을 원하는 은행 타입을 세팅하시기 바랍니다.
virtAccountType*  | 1 | **가상계좌 구분자**<br>- 0 : 일반 가상계좌, 2: 영구성 가상계좌
escrowType  | 1 | **에스크로 구분자**<br>- 0:적용 안함 1:에스크로 적용 
closeDateTime  | 14  | **마감일시**<br>- 상점아이디에 가상계좌 마감일시 세팅 옵션 설정시 필수값<br>- YYYYMMDDHHMISS
virtAccountNum*  | 15 | **가상계좌번호**<br>- 영구성 가상계좌 발급 시 필수<br>- 사업부를 통해 발급받은 가상계좌로만 사용이 가능하며, 발급이 필요할 시 사업부를 통해 연락바랍니다. 

### 응답항목(Body > data)
> 신용카드 결제 취소 응답 예시

```예시
# 성공응답
{
    "aid": "WFVVPSI00000000003100223",
    "code": "A0200",
    "message": "Success",
    "data": {
        "payload": "",
        "tid": "689449000007",
        "tradeDateTime": "20240624094405",
        "totalAmount": "1004",
        "respCode": "0000",
        "respMessage": "계좌요청완료",
        "bankType": "NONGHYUP",
        "bankName": "농협중앙",
        "virtualAccountNumb": "10185164017326",
        "accountHolder": "(T)우체국쇼핑"
    }}


# 실패응답
{
    "aid": "WFVVPSI00000000003100222",
    "code": "A0201",
    "message": "Fail",
    "data": {
        "payload": "",
        "tid": "689449000006",
        "tradeDateTime": "20240624094116",
        "totalAmount": "1004",
        "respCode": "B013",
        "respMessage": "발급거절/마감일자정보없음",
        "bankType": "NONGHYUP",
        "bankName": "농협중앙",
        "virtualAccountNumb": "",
        "accountHolder": ""
    }}

```

Name | Size | Description
--------- | ---- | -----------------------
payload  | *  | 가맹점데이터
tid  | 12  | PG거래번호
tradeDateTime | 14 | 거래일시(yyyyMMddHHmmss)
totalAmount  | 9  | 취소된금액
respCode  | 4  | 응답코드
respMessage  | 40  | 응답메시지
bankType  | *  | 은행타입
bankName  | *  | 은행명
virtualAccountNumb  | 15  | 가상계좌번호
accountHolder  | 30  | 예금주명
