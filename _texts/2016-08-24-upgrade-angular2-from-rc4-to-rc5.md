---
ID: 8
post_title: Upgrade Angular 2 from RC.4 to RC.5
author: huncode
post_excerpt: ""
layout: post
published: true
post_date: 2016-08-24 11:50:53
---
<div class="kg-card-markdown"><p>Angular 2 on upgrade from RC.4 to RC.5 marked as deprecated HTTP_PROVIDERS, added @NgModule and changed structure of root component.</p>
<p><strong>If you get notice about any <code>_PROVIDERS</code></strong></p>
<p>In RC.4 it was:</p>
<pre><code>bootstrap(AppComponent, [
  disableDeprecatedForms(),
  provideForms(),
  HTTP_PROVIDERS
]);
</code></pre>
<p>In RC.5 it looks like:</p>
<pre><code>@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    CommonModule,
    FormsModule,
    HttpModule
  ],
  providers: [],
  entryComponents: [AppComponent],
  bootstrap: [AppComponent]
})
</code></pre>
<p>As you can see all core <code>providers</code> was moved to <code>imports</code>.</p>
</div>
