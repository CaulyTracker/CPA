Cauly CPA Guide
=========================
Advertiser side Web
--------------------------
### Summary
This document describes how to integrate with Cauly Tracker When CPA campaigned. 


### Document version
| version | creating date | writer and contents |
 --- | --- | --- 
| 1.0.0 | 2017. 06. 15. | Yoon, Changju (yoonc1@fsn.co.kr) Drafting |




### Contents
- [Integration Process](#Integration-Process)
- [Integration Details](#Integration-Details)
	- [Common](#Common)		
      - [Landing Page](#LandingPage)
       	- Scripting
  - [By Campaigns](#By-Campaigns)   
      - [General Conversion Complete Page](#General-Conversion-Complete-Page)   
      	   -  Scripting
      - [Pre-Registration Complete Page](#Pre_Registration-Complete-Page)
      	   - Scripting
      - [CPS Conversion Complete Page](#CPS-Conversion-Complete-Page])
           - Scripting   

### Integration Process
1. Please contact Cauly Manager or cauly@fsn.co.kr to deal with Cauly CPA Ads.
2. Track-code will be issued. 
3. Write script guided in document into advertiser side website .
4. Cauly will verify your scripting. 
5. After successful test, Campaign starts.


### Integration Details
There are two places to write scripting
- Landing Page    : Same script for all campaigns. 
- Conversion completion Page : Differs by campaigns. 

Assume that the track code is aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee 
In the example code, aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee should be replaced with the separately issued track_code.

It is best to write the script at the end of the body tag rather than the head tag.


#### Common
##### Landing Page
This following script should be applied into landing page for all campaigns.

###### Scripting
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

#### By Campaigns
- - -
##### General Conversion Completion Page
###### Scripting
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
- - -
##### Pre_Registration Complete Page
For pre_registration campaigns, you must provide an user identifier when conversion is complete.  The identifier can be a hashed value. Note that the user identifier cannot be sent duplicately. If the same user completes the conversion more than once, only the first one should be sent. 
If user identifier is 'aaa', script is like below.

###### Scripting
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
- - -
##### CPS Conversion Complete Page
Upon completion of the CPS conversion, you must add product information (product id, price, quantity) for all purchased products.
You also need to activate the code below to display additional repurchases (disabled by default).

```javascript
purchaseEvent['purchase_type']='RE-PURCHASE';
```
###### Scripting
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
