---
ID: 10
post_title: >
  Fetch API Guide. Javascript Asynchronous
  request in 2018.
author: huncode
post_excerpt: ""
layout: post
permalink: >
  https://huncode.com/fetch-api-guide-2018/
published: true
post_date: 2017-04-23 10:11:00
---
<div class="kg-card-markdown">I still see many questions about AJAX, asynchronous callbacks and closures inside them on stackoverflow.
@skip bulshit<br>
@example of usage<br>
But now Fetch API appears on scene!
What is Fetch API
It's a high level API already implemented in all browsers (that real users, not bots, use):<br>
IE Edge, Google Chrome, Mozilla Firefox, Android Browser &amp; Chrome for Android, Safari and even iOS Safari (since 10.3 version).
For older browsers (we all like bots) there is wonderful worry-free polyfill <a href="https://github.com/github/fetch">https://github.com/github/fetch</a>
Fetch Api should replace old mammoth XHR (XMLHttpRequest) in our minds.
Instead of:
<pre><code>var xhr = new XMLHttpRequest();  
xhr.onreadystatechange = function() {  
    if (xhr.readyState == XMLHttpRequest.DONE) {
        alert(xhr.responseText);
    }
}
xhr.open('GET', 'http://test.huncode.com/get', true);  
xhr.send(null);
</code></pre>
We have awesome:
<pre><code>fetch('http://test.huncode.com/get')  
.then(function(response) {
  alert(response.text());
});
</code></pre>
So, fetch API is a new XHR, that's next?
In most of cases we use asynchronous requests to get JSON from our application API and to send forms. Let's consider this cases.
If you need an endpoint to test your application, you can use test.huncode.com:
GET, response 200: <a href="https://test.huncode.com/get">https://test.huncode.com/get</a><br>
GET, response 401: <a href="https://test.huncode.com/get/401">https://test.huncode.com/get/401</a><br>
GET, response 500: <a href="https://test.huncode.com/get/500">https://test.huncode.com/get/500</a>
POST, response 200: <a href="https://test.huncode.com/post">https://test.huncode.com/post</a><br>
POST, response 400: <a href="https://test.huncode.com/post/400">https://test.huncode.com/post/400</a><br>
POST, response 500: <a href="https://test.huncode.com/post/500">https://test.huncode.com/post/500</a>
Fetch API examples.
Case #1. Get request to JSON API. API located on the same domain.
<pre><code>fetch('http://test.huncode.com/get')  
.then(response =&gt; {
  // Check HTTP response status is 2XX
  if (response.ok) {
    return response;
  }
  // Else raise a reject to catch in our .catch function
  throw Error(response.statusText);
})
.then(response =&gt; response.json())
.then(json =&gt; {
  // our json is here
})
.catch((error) =&gt; {
  // Error in response happened
  // Check HTTP response body with error message
  console.log('ERROR!' + error.message);
});
</code></pre>
Case #2. Get request to JSON API. API located on different domain, so we need CORS.
BOOM! CORS is enabled by default, you can just take previous example.<br>
But you are awesome web developer and like to keep all the things under control.
<pre><code>fetch('http://test.huncode.com/get', {  
  mode: 'cors',
  credentials: 'include' // send cookies with the request
})
.then(response =&gt; {
  // Check HTTP response status is 2XX
  if (response.ok) {
    return response;
  }
  // Else raise a reject to catch in our .catch function
  throw Error(response.statusText);
})
.then(response =&gt; response.json())
.then(json =&gt; {
  // our json is here
})
.catch((error) =&gt; {
  // Error in response happened
  // Check HTTP response body with error message
  console.log('ERROR!' + error.message);
});
</code></pre>
Case #3. POST form to backend.
<pre><code>const data = { username: 'user', password: 'password' };  
fetch('http://test.huncode.com/post', {  
  method: 'post',
  headers: {
    'Content-Type': 'application/json' // tell the server to process sent text as JSON
  },
  body: JSON.stringify(data) // send JSON as string
})
.then(response =&gt; {
  // Check HTTP response status is 2XX
  if (response.ok) {
    return response;
  }
  // Else raise a reject to catch in our .catch function
  throw Error(response.statusText);
})
.then(response =&gt; {
 // Process response:
 // if it's a JSON: response.json()
 // if it's a text or html: response.text()
 // and do smth with response
})
.catch((error) =&gt; {
  // Error in response happened
  // Check HTTP response body with error message
  console.log('ERROR!' + error.message);
});
</code></pre>
Next step will be getting blob objects (like images) and post a true form with content type 'application/x-www-form-urlencoded'
If you are not satisfied of this article, keep reading specification: <a href="https://fetch.spec.whatwg.org/#fetch-api">https://fetch.spec.whatwg.org/#fetch-api</a>
</div>