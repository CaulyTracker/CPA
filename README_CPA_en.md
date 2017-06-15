Cauly CPA Guide
=========================
Advertiser side Web
--------------------------
### Summary
This document describes how to integrate with Cauly Tracker When CPA campaigned. 


### Document version
| version | creating date | wirter and contents |
 --- | --- | --- 
| 1.0.0 | 2017. 06. 15. | Yoon, Changju (yoonc1@fsn.co.kr) Drafting |




### Contents
- [Intergration Process](#Intergration-Process)
- [Intergration Details](#Intergration-Details)
	- [Common](#Common)		
      - [Landing Page](#Landing-Page)
        -  Scripting
  - [By Campaigns](#By-Campaigns)   
      - [General Conversion Completion Page](#General-Conversion-Completion-Page)   
        - Scripting
      - [Pre-Registration Completion Page](#Pre_Registration-Completion-Page)   
        - Scripting   
      - [CPS Conversion Completion Page](#CPS-Conversion-Completion-Page])   
        - Scripting   

### Intergration-Process
1. Please contact Cauly Manager or cauly@fsn.co.kr to deal with Cauly CPA Ads.
1. Track-code will be issued. 
1. Write script guided in document into advertiser side website .
1. Cauly will verify for your scripting. 
1. After successful test, Campaign starts.


### Intergration-Details
There are two places to write scripting
- Landing Page    : Same script for all campaigns. 
- Conversion completion Page : Differs by campaigns. 

Assume that the track code is aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee 
In the example code, aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee should be replaced with the separately issued track_code.

It is best to write the script at the end of the body tag rather than the head tag.


#### Common
##### Landing-Page
This following script should be applied into landing page for all campaigns.

###### Scripting
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
        var mTracker = new CaulyTracker();
        var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").build();
        mTracker.init(initData);
        mTracker.trackEvent('OPEN');  
</script>
```

#### By Campaigns
- - -
##### General Conversion Completion Page
###### Scripting
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
         var mTracker = new CaulyTracker();
         var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").build();
         mTracker.init(initData);
         mTracker.trackEvent('CA_CONVERSION'); 
</script>
```
- - -
##### Pre_Registration Completion Page
For pre_registration campaigns, You must provice an identifier of user when conversion is complete.  The identifier can be a hashed value. However user identifier cannot be sended duplicately . If the same user completes the conversion more than once, only the first one should be sent. 
If user identifier is 'aaa', script is like below.

###### Scripting
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
        var mTracker = new CaulyTracker();
        var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").setUserId('aaaa').build();
        mTracker.init(initData);
        mTracker.trackEvent('CA_CONVERSION');  
</script>
```
- - -
##### CPS Conversion Completion Page
Upon completion of the CPS conversion, you must add product information (product id, price, quantity) for all purchased products.
You also need to activate the code below to display additional repurchases (disabled by default).

```javascript
purchaseEvent['purchase_type']='RE-PURCHASE';
```
###### Scripting
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
         var mTracker = new CaulyTracker();
         var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").build();
          mTracker.init(initData);

          /* STAR LOOP: for all purchased product */
          mTracker.PurchaseEvent.addPurchase( "{$itemId}", "{$productPrice}", "{$productQuantity}");
          /* END LOOP */

          mTracker.PurchaseEvent.setOrder("{$orderId}", "{$orderPrice}");

          var purchaseEvent = mTracker.PurchaseEvent.build();
          /* start re-purchase,  this is for re-purchase. disable if not needed */
          //purchaseEvent['purchase_type']='RE-PURCHASE';
          /* end re-purchase */
          mTracker.trackEvent(purchaseEvent);
</script>

<script type="text/javascript">
  window._rblqueue  = window._rblqueue || [];
  /* STAR LOOP: for all purchased product  */
  _rblqueue.push(['addVar', 'orderItems', {itemId:'{$itemId}', price:'{$productPrice}', quantity:'{$productQuantity}'}]);
  /* END LOOP */
</script>

<script type="text/javascript">
window._rblqueue  = window._rblqueue || [];
_rblqueue.push(['setVar','cuid','aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee']);
_rblqueue.push(['setVar','device','{$device}']);
_rblqueue.push(['setVar','orderId','{$orderId}']);
_rblqueue.push(['setVar','orderPrice','{$orderPrice}']);
_rblqueue.push(['setVar','userId','{$userId}']);		// optional
_rblqueue.push(['track','order']);
setTimeout(function() {
  (function(s,x){s=document.createElement('script');s.type='text/javascript';
  s.async=true;s.defer=true;s.src=(('https:'==document.location.protocol)?'https':'http')+
    '://assets.recobell.io/rblc/js/rblc-apne1.min.js';
  x=document.getElementsByTagName('script')[0];x.parentNode.insertBefore(s, x);})();
}, 0);
</script>
```

| Field Name | Nullable | Description | 
| ---------- | -------- | ----------- |
| {$device} | NOT NULL | User device category.   It should have one of the following four values.<br/>PW : PC Web<br/> MW : Mobile Web<br/> MI : MobileiOS<br/> MA : Mobile Android |
| {$itemId} | NOT NULL | Purchased ID (Product Code). <br/>The product ID should be the same as the product ID delivered from the product detail page.. |
| {$productPrice} | NOT NULL | The price of the item |
| {$productQuantity} | NOT NULL | The number of items  |
| {$orderId} | NOT NULL |  Ordered payment ID |
| {$orderPrice} | NOT NULL | The price of the order |
| {$userId} | NULL | Login ID of user who visited (optional) . Due to legal issue  <br/>  It is common to put a HASH value. |
