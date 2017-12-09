---
ID: 9
post_title: >
  Object.assign performance on using with
  collections.
author: huncode
post_excerpt: ""
layout: post
permalink: https://huncode.com/?p=9
published: true
post_date: 2017-03-08 10:09:00
---
<div class="kg-card-markdown"><p>With ES2016 we have many things write shorter and look better.</p>
<p>Small experiment of using <code>Object.assign</code>.</p>
<p>I have tried to use it in reduce functions that's convert collection to index object. For example to index by id with and without Object.assign:</p>
<pre><code class="language-js">collection.reduce((items, item) =&gt; {  
  items[item.id] = item;
  return items;
}, {});
collection.reduce((items, item) =&gt; Object.assign(items, { [item.id]: item }), {});  
</code></pre>
<p>What about performance?</p>
<p>I use simple console test with <code>console.time()</code> for syncronious operation to check their performance.</p>
<p>Example test</p>
<p>First lets generate 10000 random items collection:</p>
<pre><code>const collection = [...Array(10000)]  
  .map((item, index) =&gt; ({id: index, value: Math.random()}));
Count reduce execution time without Object.assign:

console.time('test');  
collection.reduce((col, item) =&gt; {  
  col[item.id] = item;
  return col;
}, {});
console.timeEnd('test');
</code></pre>
<p>Result test: 0.797119140625ms</p>
<p>Count reduce execution with Object.assign:</p>
<pre><code>console.time('test');
collection.reduce((col, item) =&gt; Object.assign(col, { [item.id]: item }), {});
console.timeEnd('test');
</code></pre>
<p>Result: test: 18.228271484375ms</p>
<p>Total</p>
<p>Object.assign method is still not optimised well and you should carefully use it on huge collections.</p>
<p>Tested in Chrome Canary version 59.0.3035.0</p>
</div>