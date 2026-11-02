---
layout: post
title: "HAProxy - Blocking those pesky vuln-scanners"
date: 2021-02-25 15:02:45 +0000
author: NoLifeKing
tags:
- haproxy
---

<p>So, after spending almost 4 days.. yes, four days.. I managed to finally get something working, not exactly like I wanted it, but close enough..</p><p>Reading through lots of blog posts and gists around the internet about how to setup the "perfect detection and blocking"-system in your HAProxy instance, I finally came up with this little snippet, that does most of the work</p><!--more--><!--kg-card-begin: markdown--><pre><code class="language-plaintext">acl    is_spammy_mcspam_client    src_http_err_rate gt 0

tcp-request    inspect-delay 10s
tcp-request    content silent-drop if is_spammy_mcspam_client

http-request    track-sc0    src if { path_beg -i -f /haproxy-json/default-blocked-paths.lst } !{ src -f /haproxy-json/whitelist-ipranges.lst }
http-request    silent-drop    if    is_spammy_mcspam_client

stick-table    type ip size 200k expire 10m store http_err_rate(1d)
</code></pre>
<!--kg-card-end: markdown--><p>This is all placed in the frontend you want to protect, and then in the files <code>default-blocked-paths.lst</code> and <code>whitelist-ipranges.lst</code> I've put endpoints that are usually used when scanning for vulnerable endpoints in your website, or if someone put their entire <code>.git</code>-folder there, and things like that.</p><p>Do note that I'm only logging where you actually get an error, because in my case, we don't have the paths that people tend to access, so we only get 404s, which we then track the IP for each request to one of those endpoints, unless they're in our whitelist.</p>