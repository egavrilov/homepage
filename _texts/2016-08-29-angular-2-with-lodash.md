---
ID: 6
post_title: Angular 2 with lodash.
author: huncode
post_excerpt: ""
layout: post
published: true
post_date: 2016-08-29 12:44:32
---
<div class="kg-card-markdown"><p>Simplest way to add lodash to your project is to install it with npm</p>
<pre><code>npm install lodash --save
</code></pre>
<p>and add to typescript file</p>
<pre><code class="language-es6">import * as _ from 'lodash'
</code></pre>
<p>But it means, that you get extra 69 Kb (23 Kb gzipped) in your build file. It's to much if you use only couple of functions and not all the library.</p>
<p>I use Angular CLI Webpack and it's very easy to use only needed functions from lodash.</p>
<p>First install ES6 lodash npm module</p>
<pre><code>npm install lodash-es --save
</code></pre>
<p>After that add typings definitions from @types repository</p>
<pre><code>npm install @types/lodash --save-dev
</code></pre>
<p>And finally in typescript file:</p>
<pre><code>import { merge, mergeWith } from 'lodash';
</code></pre>
<p>Know you have tiny pieces of lodash included in your project instead of all the library.</p>
</div>
