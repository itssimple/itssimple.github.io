---
layout: post
title: "A wrapper to get data about your TCP connections"
date: 2022-07-11 15:32:43 +0000
author: NoLifeKing
tags:
- netstat
- nuget
---

<p>After looking around on the internet for, what felt like, days.. I decided to put together this small wrapper package, to be able to get network info (tcp connections, like netstat).</p><p>Gonna use it to be able to graph the state of our servers connection states (debugging port exhaustion), so we can see if our fixes lowers the amount of TIME_WAIT connections that never seems to close.</p><!--more--><p>Package can be found at the link below:</p><p><a href="https://www.nuget.org/packages/ItsSimple.NetStatData/1.0.0">https://www.nuget.org/packages/ItsSimple.NetStatData/1.0.0</a></p>





