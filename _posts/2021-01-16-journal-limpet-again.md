---
layout: post
title: "Journal Limpet, again!"
date: 2021-01-16 08:42:43 +0000
author: NoLifeKing
tags:
- journal limpet
- elite dangerous
---

<p>So, the vacation I had during christmas, I spent a few days on actually building up <a href="https://journal-limpet.com">Journal Limpet</a>, and I'm happy to say that I already have over 30+ users with 600+ journals and almost 1.3 million lines of journals stored.</p><p>So what happened since we published our last post?</p><!--more--><p>Well, for starters we:</p><ul><li>Built the entire backend that handles authentication and refreshing API tokens</li><li>Redid the entire database class, to use MSSQL instead of Postgresql (it's easier for me)</li><li>Added a small Redis-cache to keep track of gamestate for our EDDN and EDSM journal publishers</li><li>Built the EDDN publisher, that sends your journals over to EDDN automatically</li><li>Built the EDSM publisher, that.. just like above. Just enter your API credentials</li></ul><p>And now, all I have to do, is wait for more users, so I can see where I have any potential bottlenecks in performance, so I can hopefully fix that.</p><p>One of the things I will have to fix is actually the database, sooner or later, because the SQL Server Express limits the amount of memory I can use, how big my database can be (10GB should be quite enough for a while though) and how many CPU cores it can utilize.</p><p>If I could choose, I would gladly pay for a license for SQL Server, but for a project that I don't intend to get any money from, it's kinda expensive. Maybe I'll reach out to Microsoft and ask them for guidance or maybe even an Open Source license! (one can dream)</p>