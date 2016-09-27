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



### 목차
- [연동 절차](#연동-절차)
- [연동 상세](#연동-상세)
	- [랜딩 페이지](#랜딩-페이지)
		- 스크립트 삽입
	- [전환 완료 페이지](#전환-완료-페이지)
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

#### 랜딩 페이지
##### 스크립트 삽입
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
        var mTracker = new CaulyTracker();
        var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").build();
         mTracker.init(initData);
         mTracker.trackEvent('OPEN');  
</script>
```

#### 전환 완료 페이지
##### 스크립트 삽입
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
         var mTracker = new CaulyTracker();
         var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").build();
          mTracker.init(initData);
          mTracker.trackEvent('CA_CONVERSION'); 
</script>
```
