---
layout: post
title: "First impressions of Ghost"
date: 2020-04-23 04:42:52 +0000
author: NoLifeKing
tags:
- blog
- node
- nginx
- docker
- cron
- javascript
---

<p>First of all, I just want to say, writing posts is really neat.</p><p>You have this clean editor with nothing to disturb you, and you pretty much have the WYSIWYG-editor, a word counter. That's it! And that's about all you need to get started.</p><!--more--><p>And whenever you start a new paragraph, you can select if you want to add something extra there, like importing a video from YouTube, an image from Instagram or anything.</p><p>Anyway, this is not an ad for Ghost, more about my first impressions about it.</p><p>I started using Ghost since it looked really neat, and from the demo webpage, had lot of promise, I had high hopes for it.</p><p>Setup was a breeze, just installed a Docker-image, did some few tweaks and set it up through a reverse proxy in nginx. (Actual config below)</p><figure class="kg-card kg-code-card"><pre><code class="language-plain">server {
        server_name *.nolifeking85.tv nolifeking85.tv;

        listen 443 ssl http2;
        listen [::]:443 ssl http2;

        location / {
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-NginX-Proxy true;
                proxy_pass http://127.0.0.1:2368/;
                proxy_ssl_session_reuse off;
                proxy_set_header Host $http_host;
                proxy_cache_bypass $http_upgrade;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_read_timeout 900;
                proxy_redirect off;
        }
}</code></pre><figcaption>Pretty simple, am I right?</figcaption></figure><p>Now, the real reason why I wanted to try out Ghost, was both for my normal dayjob at <a href="https://www.multinet.com">MultiNet Interactive AB</a>, so we could build a developer portal, that was easily extendable, but still powerful while retaining performance. And as a replacement for the CMS used for handling the less static pages that we have on <a href="https://fuelrats.com">The Fuel Rats Mischief</a> website, because we don't like the current one, but haven't found a good replacement for it, as of yet.</p><p>Here I noticed the first thing missing.. when I read Ghost website about features and everything, it all looked really good. I mean, it still is really good. But I'm missing what I feel is a key feature, and that's the easy way to build plugins/apps for it.</p><p>Since I'm a content creator (Twitch Streamer), I thought that I would love to have some easy way for me to just add a module that runs behind the scenes and fetches my online status on Twitch, to see if I'm live or not. Sounds easy, right? So I started reading <em>all</em> the documentation and found that the apps-support suddenly seemed to have vanished (at least the information on how to create them have).</p><p>But since, I'm also a developer, I decided not to give up, because I don't want to sully my reputation as a developer.</p><p>So, first of. I wanted some kind of script to check whether I'm Live or not on Twitch, so we just wrote a simple JavaScript to fetch that and save it to a file.</p><figure class="kg-card kg-code-card"><pre><code class="language-javascript">const fetch = require('node-fetch');
const fs = require('fs');

var x = fetch(
  'https://api.twitch.tv/helix/streams?user_login=nolifeking85',
  {
    headers: {
      'Client-ID': ENV.TWITCH_CLIENTID
    }
  }
);

x.then(x2 =&gt; x2.json())
  .then(json =&gt; {
    fs.writeFile(
      ENV.TWITCH_JSONFILE,
      JSON.stringify(json),
      function (error) {
        if(error) {
          return console.error(error);
        }
      }
    );
  }
);</code></pre><figcaption>Again, really simple code, since it's a really simple request. (It's not even this well formatted in production)</figcaption></figure><p>And then I went to type in <code>crontab -e</code>, just to see that <code>cron</code> is in fact not installed, so we head off to install that as well. (I can tell you this, things like <code>ps</code>, <code>uptime</code> are missing too), and then we just figured out what user we should run this script as (for correct permissions and all) by looking into the <code>/home</code>-folder, so that we can run the cron job as that user.</p><p>So what I have left to do today, when work is done (I work remote right now during these Corona times between 08.00-17.00 (but I tend to start at ~07.30 and sometimes end ~20.00)), I will write a small javascript that I will put in my footer of the webpage, that will read said file from disk, and edit the nav menu item with the appropriate styles. :)</p><p>So while I waited for my lunch to cool down enough for me to eat it, I took my time to write some fugly JavaScript in the code injection for the footer. View all the magnificent code! (Will be edited later, since I don't have enough data to handle this yet)</p><figure class="kg-card kg-code-card"><pre><code class="language-javascript">    function checkIfLiveOnTwitch() {
        fetch('https://nolifeking85.tv/content/images/twitch.json').then(f =&gt; f.json()).then(json =&gt; handleTwitchJson(json));
    }

    function handleTwitchJson(json) {
        const navLiveStreamItem = document.querySelector('.nav-stream a');

        if (json.data.length !== 0) {
            const streamData = json.data[0];

            if(streamData.user_name !== 'NoLifeKing85' || streamData.type !== 'live') return;

            const liveIndicator = $('&lt;div class="live-indicator"&gt;LIVE&lt;/div&gt;');

            liveIndicator.prop('title', streamData.title);
            liveIndicator.text(`LIVE (${streamData.viewer_count})`);

            if(document.querySelectorAll('.nav-stream .live-indicator').length === 0) {
              navLiveStreamItem.prepend(liveIndicator[0]);
            }
        } else {
            /* Offline indicator? Naaaah */
            if(document.querySelectorAll('.nav-stream .live-indicator').length === 1) {
                $('.nav-stream .live-indicator').remove();
            }
        }
    }

    (function() {
        checkIfLiveOnTwitch();
        setInterval(checkIfLiveOnTwitch, 10000);
    })();</code></pre><figcaption>Ain't it a beauty? Just poll the file I create/update with the cron job in the background!</figcaption></figure><p>And when I feel advanced enough, I might change this into a websocket-thing instead, so that I add a websocket that serves the above JSON-file, so I can act on "live" updates. But for now, we will have to do with polling.</p>