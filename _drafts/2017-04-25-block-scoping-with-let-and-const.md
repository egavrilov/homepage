---
ID: 12
post_title: Block scoping with let and const
author: huncode
post_excerpt: ""
layout: post
published: true
post_date: 2017-04-25 10:16:00
---
<div class="kg-card-markdown"><p>@skip the bullshit<br>
@scroll to examples</p>
<p>Since JavaScript was created we have only one way to declare variable - with a var statement.</p>
<p>var huncode = 'Someone who writes fast and damn simple code';<br>
It vas several problems with var:</p>
<p>If run outside function statements it declares in global namespace (developers writes couple of petabytes of articles and comments of how to prevent this. It was the first question on my first job interview).<br>
Recreates variable in current scope if it's already exists. Millions of dollars was spent to pay developers who lose an hour trying to figure out why value isn't one as expect.<br>
...there are more, but I'm too lazy to continue (ping me and I will finish the list for sure).<br>
Examples</p>
<p>Closure inside loop</p>
<p>Before block scopes it was a real problem to keep value inside loop or setTimeout, and we have to use tricky solutions, like:</p>
<pre><code>var closures = [];

for (var i = 0; i &lt; 5; i++) {  
  closures[i] = (function(storedIndex) {
    return function () {
      console.log('Current value is', storedIndex);
    };
  }(i));
}

closures.forEach(function (closure) {  
  closure();
});
</code></pre>
<p>But now with ES201x we have nice solution of the problem for cool guys.</p>
<pre><code>const closures = [];  
for (let i = 0; i &lt; 5; i++) {  
  closures[i] = () =&gt; {
    console.log(`Current value is ${i}`);
  };
}

closures.forEach(closure =&gt; closure());  
</code></pre>
<p>Bonus: const and let with switch block.</p>
<p>If one will try to use const or let inside switch-case statement &quot;Uncaught SyntaxError: Identifier has already been declared&quot; would be raised.</p>
<pre><code>const total = 1;  
switch(total) {  
  case 'No total':
    const message = 'Message for no total';
    console.log(message);
    break;
  case 1:
    const message = 'Message for total == 1';
    console.log(message);
    break;
}
</code></pre>
<p>It happens because &quot;block scope&quot; in JavaScript just means &quot;inside curved braces&quot;.<br>
And simply adding curved braces to case will solve the error:</p>
<pre><code>const total = 1;  
switch(total) {  
  case 'No total': {
    const message = 'Message for no total';
    console.log(message);
    break;
  }
  case 1: {
    const message = 'Message for total == 1';
    console.log(message);
    break;
  }
}
</code></pre>
</div>
