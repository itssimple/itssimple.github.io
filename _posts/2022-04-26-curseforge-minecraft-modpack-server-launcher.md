---
layout: post
title: "CurseForge Minecraft Modpack Server Installer"
date: 2022-04-26 04:57:03 +0000
author: NoLifeKing
tags:
- curseforge
- minecraft
- modpack
- server
- cf-mc-server
---

<p>So, I've seen a lot of people struggle with getting modpack servers working, even if the instructions are very clear from the modpack makers, no matter how much help they get from the <a href="https://discord.com/invite/curseforge">CurseForge Discord</a>..</p><!--more--><p>And with that, I started a (yet another) little project of mine, first of all, because I wanted one myself, to see if I could pull it off, using nothing but the available APIs, and some code of mine.. spoiler, I made it work.</p><p>First off, I'm gonna say it, it's not perfect, there will be modpacks that it will fail to at least <em>start</em>, because of the nature of Minecraft modding, where the devs doesn't add code to bail out if they are intended as client-side mods only. And the reason this software will fail because of that, is because they are not tagged as client-only mods (you can't mark them as such).</p><p>And, no it's not a GUI based application, it's a CLI (Command Line Interface), to make it usable on most platforms.</p><p>Edit: Previously, we didn't have a macOS version, but with 1.0.1, we have support for macOS as well!</p><p>But, if an image speaks more than thousand words, what would a video do then?</p><figure class="kg-card kg-embed-card kg-card-hascaption"><iframe width="200" height="113" src="https://www.youtube.com/embed/Uy7cILUgh6U?feature=oembed" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><figcaption>A small (old) demo video on what the installer looked like during development</figcaption></figure><p>The project is of course open source, and can be found in the <a href="https://github.com/CurseForgeCommunity/cf-mc-server">CurseForgeCommunity GitHub organization</a>. So, if you have any questions, feature requests or bug reports, be sure to get them in there!</p><p>We also have a documentation site available for this project, which will tell you the absolute basics on how to use it. And it's available <a href="https://curseforgecommunity.github.io/cf-mc-server/">here</a>.</p><p>Now, get out there, create your own server, and good luck with the mining! &lt;3</p>