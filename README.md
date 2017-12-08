Cauly CPA 광고 가이드
=========================
광고주 Web
--------------------------
### 개요
이 문서는 광고주가 Cauly 와 CPA 광고를 집행할 때 tracker 를 삽입하는 방법에 대해서 설명하는 문서입니다.

### 문서 버전 
| 문서 버전 | 작성 날짜 | 작성자 및 내용|
 --- | --- | --- 
| 1.0.0 | 2016. 06. 02. | 권순국(nezy@fsn.co.kr) 초안 작성|
| 1.0.1 | 2017. 02. 17. | 권순국(nezy@fsn.co.kr) 사전예약 캠페인 추가|
| 1.0.2 | 2017. 04. 12. | 황우현(hwangwoohyun@fsn.co.kr) 회원가입 캠페인, CPS 캠페인 추가|



### 목차
- [연동 절차](#연동-절차)
- [연동 상세](#연동-상세)
	- [일반](#일반)		
		- [랜딩 페이지](#랜딩-페이지)
			- 스크립트 삽입
		- [전환 완료 페이지](#전환-완료-페이지)
			- 스크립트 삽입
	- [사전예약 캠페인](#사전예약-캠페인)
		- [사전예약 랜딩 페이지](#사전예약-랜딩-페이지)
			- 스크립트 삽입
		- [사전예약 전환 완료 페이지](#사전예약-전환-완료-페이지)
			- 스크립트 삽입
	- [회원가입 캠페인](#회원가입-캠페인)
		- [회원가입 랜딩 페이지](#회원가입-랜딩-페이지)
			- 스크립트 삽입
		- [회원가입 전환 완료 페이지](#회원가입-전환-완료-페이지)
			- 스크립트 삽입
	- [CPS 캠페인](#cps-캠페인)
		- [CPS 랜딩 페이지](#cps-랜딩-페이지)
			- 스크립트 삽입
		- [CPS 전환 완료 페이지](#cps-전환-완료-페이지)
			- 스크립트 삽입

### 연동 절차
1. Cauly 담당자 혹은 cauly@fsn.co.kr로 연락하여 Cauly CPA 광고 집행에 대해서 협의합니다.
1. 협의 완료 후, track_code 를 발급받습니다.
1. track_code 를 포함한 tracker 코드를 사이트의 페이지에 삽입합니다.
1. 페이지 삽입 이후 연동이 되었는지 Cauly 에서 테스트를 진행합니다.
1. 테스트가 완료되면 광고를 집행합니다.


### 연동 상세
tracker 스크립트의 삽입 위치는 아래 2군데입니다.
- 랜딩 페이지
- 전환 완료 페이지

Cauly 에서 발급한 track_code 를 aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee 라고 가정하겠습니다.
예제 코드에서 aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee 부분은 따로 발급 받은 track_code 로 대체하여야 합니다.

스크립트는 head 태그 보다는 body 태그 안쪽의 마지막 부분에 삽입하는 것이 좋습니다.

#### 일반
##### 랜딩 페이지
###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['event_name','OPEN']);
  _paq.push(['send_event']);
  (function()
  { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); })();
</script>
```

##### 전환 완료 페이지
###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['event_name','CA_CONVERSION']);
  _paq.push(['send_event']);
  (function()
  { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); })();
</script>
```
#### 사전예약 캠페인
##### 사전예약 랜딩 페이지
###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['event_name','OPEN']);
  _paq.push(['send_event']);
  (function()
  { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); })();
</script>
```

##### 사전예약 전환 완료 페이지
###### 스크립트 삽입
사전 예약의 경우 전환 완료 시, user 를 식별할 수 있는 식별자를 넣어주어야 합니다. sha1 hash 된 값으로 보내는 것을 권장합니다. 그리고 user 식별자를 중복으로 보내서는 안됩니다. 같은 user 가 2번 이상 전환 완료했다면 최초 1번의 전환만 보내져야 합니다.
user 식별자가 '01011112222' 라면 코드는 아래와 같습니다.
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/cpa/util_sha1.js" ></script>
<script type="text/javascript">
  var strUser = '01011112222';      
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['user_id',SHA1(strUser)]); // option
  _paq.push(['event_name','CA_CONVERSION']);
  _paq.push(['send_event']);
  (function() { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); }
  )();
        
</script>
```

#### 회원가입 캠페인
##### 회원가입 랜딩 페이지
###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['event_name','OPEN']);
  _paq.push(['send_event']);
  (function()
  { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); })();
</script>
```

##### 회원가입 전환 완료 페이지
###### 스크립트 삽입
회원가입의 경우 전환 완료 시, user 를 식별할 수 있는 식별자를 넣어주어야 합니다. sha1 hash 된 값으로 보내는 것을 권장합니다. 그리고 user 식별자를 중복으로 보내서는 안됩니다. 같은 user 가 2번 이상 전환 완료했다면 최초 1번의 전환만 보내져야 합니다.
user 식별자가 'aaaa' 라면 코드는 아래와 같습니다.
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/cpa/util_sha1.js" ></script>
<script type="text/javascript">
  var strUser = '01011112222';      
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['user_id',SHA1(strUser)]); // option
  _paq.push(['event_name','CA_CONVERSION']);
  _paq.push(['send_event']);
  (function() { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); }
  )();
        
</script>
```

#### CPS 캠페인
##### CPS 랜딩 페이지
###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['event_name','OPEN']);
  _paq.push(['send_event']);
  (function()
  { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); })();
</script>
```

##### CPS 전환 완료 페이지
###### 스크립트 삽입
CPS 전환 완료시, 구매한 모든 상품에 대해 상품정보(상품id, 가격, 수량)를 추가해야 합니다.
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['user_id','{$userId}']); // option
  _paq.push(['event_name','PURCHASE']);
  _paq.push(['order_id','{$orderId}']);
  _paq.push(['order_price','{$orderPrice}']);
  var products_q = [];

  /* STAR LOOP: 구매한 모든 상품에 대해 */
  products_q.push({'product_id': '{$itemId}','product_price':'{$productPrice}','product_quantity':'{$productQuantity}'});
  /* END LOOP */

  _paq.push(['product_infos',products_q]);
  _paq.push(['send_event']);    
  (function(){ var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); }
)();
</script>

```

| Field Name | Nullable | Description | 
| ---------- | -------- | ----------- |
| {$itemId} | NOT NULL | 결제된 상품 ID (상품코드). <br/>이때의 상품ID는 상품상세 페이지에서 전달한 상품ID와 동일한 것이어야 한다. |
| {$productPrice} | NOT NULL | 결제된 상품의 가격 |
| {$productQuantity} | NOT NULL | 결제된 상품의 갯수 |
| {$orderId} | NOT NULL | 결제완료된 주문 ID |
| {$orderPrice} | NOT NULL | 결제완료된 주문의 가격 |
| {$userId} | NULL | 방문한 유저의 로그인 아이디 (optional) 법적이슈의 문제로<br/> HASH 값을 넣어주는 것이 일반적이다. |
