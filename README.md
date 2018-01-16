# Google-Analytics

https://developers.google.com/analytics/devguides/collection/analyticsjs/tasks<br>

* local http request 1

``` javascript 
<script>
  
  ga('create', 'UA-80008755-1', 'auto');
  
 ga(function(tracker) {


  // Modifies sendHitTask to send a copy of the request to a local server after
  // sending the normal request to www.google-analytics.com/collect.
  tracker.set('sendHitTask', function(model) {
    
    var xhr = new XMLHttpRequest();
    xhr.open('POST', '/localhits' + '?' + model.get('hitPayload'), true);
    xhr.send();
  });
});
  
  ga('send', 'pageview');

</script>
```



* local http request 2

``` javascript 
<script>
    (function(i, s, o, g, r, a, m) {
        i['GoogleAnalyticsObject'] = r;
        i[r] = i[r] || function() {
            (i[r].q = i[r].q || []).push(arguments)
        }, i[r].l = 1 * new Date();
        a = s.createElement(o),
            m = s.getElementsByTagName(o)[0];
        a.async = 1;
        a.src = g;
        m.parentNode.insertBefore(a, m)
    })(window, document, 'script', 'https://www.google-analytics.com/analytics.js', 'ga');

    ga('create', 'UA-xxxxxxx-y', 'auto');
    ga(function(tracker) {

        // Grab a reference to the default sendHitTask function.
    var originalSendHitTask = tracker.get('sendHitTask');

        // Modifies sendHitTask to send a copy of the request to a local server after
        // sending the normal request to www.google-analytics.com/collect.
    tracker.set('sendHitTask', function(model) {
            originalSendHitTask(model);
            var xhr = new XMLHttpRequest();
            xhr.open('POST', '/localhits.gif' + '?' + model.get('hitPayload'), true);
            xhr.send();
        });
    });
    ga('send', 'pageview');
</script>
```


* local http request 3

``` javascript 
<script>

ga(function(tracker) {

  // Grab a reference to the default sendHitTask function.
  var originalSendHitTask = tracker.get('sendHitTask');

  // Modifies sendHitTask to send a copy of the request to a local server after
  // sending the normal request to www.google-analytics.com/collect.
  tracker.set('sendHitTask', function(model) {
    originalSendHitTask(model);
    var xhr = new XMLHttpRequest();
    xhr.open('POST', '/localhits', true);
    xhr.send(model.get('hitPayload'));
  });
});
</script>
```
