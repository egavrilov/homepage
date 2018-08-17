---
ID: 11
post_title: Docker Mail Server
author: huncode
post_excerpt: ""
layout: post
published: true
post_date: 2017-04-24 10:13:00
---
<div class="kg-card-markdown"><p>As simple as install docker component on your server.<br>
Previously I've used laa/dockermail but after switched to more simple docker container with docker-compose</p>
<p>Let's go:<br>
<a href="https://github.com/tomav/docker-mailserver">https://github.com/tomav/docker-mailserver</a></p>
<p>Install docker on your server;<br>
And install docker-compose after;</p>
<p>Create new folder for your mailserver configuration<br>
<code>mkdir -p ~/config/mail</code></p>
<p>Create docker-compose.yml inside created folder<br>
<code>touch ~/config/mail/docker-compose.yml</code></p>
<p>Put configuration inside it with your favorite text editor.</p>
<pre><code>version: '2'

services:  
  mail:
    image: tvial/docker-mailserver
    hostname: mail
    container_name: mail
    ports:
    - &quot;25:25&quot;
    - &quot;143:143&quot;
    - &quot;587:587&quot;
    - &quot;993:993&quot;
    volumes:
    - maildata:/var/mail
    - ./config:/tmp/docker-mailserver
    - /etc/letsencrypt:/etc/letsencrypt
    environment:
      SSL_TYPE: letsencrypt
    logging:
      options:
        max-size: &quot;10m&quot;
    restart: always
volumes:  
  maildata:
    driver: local
</code></pre>
<p>But using mail server without webmail isn't very comfort, so I adding rainloop to my config.</p>
<pre><code>  rainloop:
    image: solidnerd/rainloop
    container_name: mail_rainloop
    ports:
      - &quot;9001:80&quot;
    volumes:
      - rainloop:/var/www/rainloop/data
    logging:
      options:
        max-size: &quot;10m&quot;
    restart: always
    cpuset: &quot;1&quot;
volumes:  
  rainloop:
    driver: local
</code></pre>
<p>Full configuration will look:</p>
<pre><code>version: '2'

services:  
  mail:
    image: tvial/docker-mailserver
    hostname: mail
    container_name: mail
    ports:
    - &quot;25:25&quot;
    - &quot;143:143&quot;
    - &quot;587:587&quot;
    - &quot;993:993&quot;
    volumes:
    - maildata:/var/mail
    - ./config:/tmp/docker-mailserver
    - /etc/letsencrypt:/etc/letsencrypt
    environment:
      SSL_TYPE: letsencrypt
    logging:
      options:
        max-size: &quot;10m&quot;
    restart: always
  rainloop:
    image: solidnerd/rainloop
    container_name: mail_rainloop
    ports:
      - &quot;9001:80&quot;
    volumes:
      - rainloop:/var/www/rainloop/data
    logging:
      options:
        max-size: &quot;10m&quot;
    restart: always
    cpuset: &quot;1&quot;
volumes:  
  maildata:
    driver: local
  rainloop:
    driver: local
</code></pre>
<p>Now go to your folder and run containers</p>
<pre><code>cd ~/config/mail  
docker-compose up -d
</code></pre>
<p>Now you can open webmail on<br>
<a href="http://your-server:9001/">http://your-server:9001/</a></p>
</div>
