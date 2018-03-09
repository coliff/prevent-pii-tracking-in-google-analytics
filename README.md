# Prevent PII from being tracking in Google Analytics

Google don't allow PII (Personally Identifiable Information) to be tracked in Google Analytics. You can have your Google Analytics account suspeneded if you don't abide by the rules.

Google provide some helpful [Best Practises information](https://support.google.com/adsense/answer/6156630?hl=en), but their suggestions often rely on rewriting your web application so that PPI aren't displayed in the URL.

This work-around script works by only including Google Analytics tracking snippet if the URL **does not** include `email=`, `username=` or `password=` strings. The exact strings could easily be modified to suit your needs.

``` html
<script>
  window.ga=function(){ga.q.push(arguments)};ga.q=[];ga.l=+new Date;
  ga('create','UA-XXXXX-Y','auto');ga('send','pageview')
</script>
<script>
  if(location.href.match(/(?:\b|_)(?:username|email|password)(?:\b|_)/i) > -1){
  document.write('<script src="https://www.google-analytics.com/analytics.js" aysnc defer><\/script>');
  }
</script>
```

See demo at:
[https://coliff.github.io/prevent-pii-tracking-in-google-analytics/demo.htm](https://coliff.github.io/prevent-pii-tracking-in-google-analytics/demo.htm) - this loads Google Analytics as normal

If you include params with PPI in the URL though, Google Analytics will not load:

- [demo.htm?username=redacted%40example.com&password=Z0CS9](https://coliff.github.io/prevent-pii-tracking-in-google-analytics/demo.htm?username=redacted%40example.com&password=Z0CS9)

- [demo.htm?userName=redacted%40example.com&token=9234](https://coliff.github.io/prevent-pii-tracking-in-google-analytics/demo.htm?userName=redacted%40example.com&token=9234)

- [demo.htm?email=redacted%40example.com&token=%3%tX](https://coliff.github.io/prevent-pii-tracking-in-google-analytics/demo.htm?email=redacted%40example.com&token=%3%tX)


Note; the optimized Google Analytics snippet is from [HTML5Boilerplate](https://github.com/h5bp/html5-boilerplate/blob/master/src/index.html)

<script>
  if(location.href.match(/(?:\b|_)(?:username|email|password)(?:\b|_)/i) > -1){
  document.write('<script src="https://www.googleadservices.com/pagead/conversion.js"><\/script>');
  }
</script>
