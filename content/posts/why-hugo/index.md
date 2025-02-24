---
title: "Why Hugo?"
summary: Decision making behind choosing Hugo, for the Luanti Docs Project
date: 2025-02-23
author: ["wsor4035"]
cover:
    image: mountain-range-and-forest-during-daytime.jpg
    hiddenInList: true
    caption: by Florian van Duyn - [Source](https://unsplash.com/photos/mountain-range-and-forest-during-daytime-BR1WANLLpDU)
---

## Prequel

So I think this blog post requires a prequel, or a disclaimer if you would. So first things first this blog post is written mostly about my decision making 
process and options when deciding what to use for the [Luanti Docs Project](https://github.com/luanti-org/docs.luanti.org). Your own project maybe have different 
requirements/aspirations/wants, etc so some or all of this may not apply. That all said, hope you find some value from this post.

## Scope

Before the project came to be, [Luanti](https://github.com/luanti-org/luanti) had three main documentation sites, ones that people used anyways. Those are/where:
* [api.luanti.org](https://api.luanti.org/)
* dev.luanti.org
* wiki.lunati.org

The first one, api.luanti.org is a generated nice form for the [lua_api.md](https://github.com/luanti-org/luanti/blob/master/doc/lua_api.md) documentation file for 
those who prefer it in a nice grouped form. The latter two where two [Media Wiki](https://www.mediawiki.org/wiki/MediaWiki) hosted by [c55](https://github.com/celeron55) 
that where known for many issues, such as: outdated content, very slow or not working at all, outdated, getting accounts was very had and painful, spam issues, etc.

Further more Luanti has grown from being a game to more of a game engine, so the need for two separate wikis was diminished. With that in mind some goals where merging 
the two wikis, using stable hosting, ease of access for people to contribute, avoiding spam, and many more not relevant to this blog post. For the tech stack two main points 
where that the docs project probably should use static site - to aid in being able to run anywhere, ease of local dev, etc - and that it should be focused on the content 
more than implementing a tech stack and maintaining it.

## Competitors

At this point, you might be very bored of reading the first two sections, or you hopped straight here :p. In any rate, before declaring something the best, should probably 
look at the options right? After all everything has trade offs. In the case of the docs project, three main options appeared(outside of Hugo):

### * Rolling something custom

You may be wondering, if you read the [scope](#scope) section, which talked about focusing on content over tech stack why this is even and option. ....And to be fair, you 
are mostly right, *however*...... it is very simple to grab a library for converting markdown, and make a simple template that wraps that in a header and footer. That said this 
option was rather quickly dismissed, as it could quickly climb in scope, adding things like open graph tags, table of contents, search, etc. Additionally it would always incur 
some tech stack maintenance in upgrading the libraries, making sure nothing broke, etc. 

### * Jekyll

[Jekyll](https://jekyllrb.com/) is probably one of the oldest, still used static site generators. Being the oldest, that can cut both ways, perhaps leading to maturity, a better 
feature set, more support, etc - but it can also mean that its lost the ability to be fast and nimble, lack support for new standards/features, etc. I'll leave it up to the reader 
as to which is true, perhaps even it is in the eye of the beholder. Some positives that it does have, is that it has wide support, has themes (a listing isn't nicely integrated with 
the project it seems, they link out to other listings), etc. In the negatives it requires a plugin for translation, is written in ruby (no offense to the ruby devs out there, but the 
[Stack Overflow Survey](https://survey.stackoverflow.co/2024/technology/#1-programming-scripting-and-markup-languages) percentages aren't up there), has been a personal sore point of 
pain in the past (subjective I know). All that said it is a valid option.

### * Astro

[Astro](https://astro.build/) is a relative newcomer at three years old, however it certainly packs a [punch](https://docs.astro.build/en/concepts/why-astro/). Some positives are 
that it has quick access to themes, is in the JavaScript ecosystem(which has a wide breadth of packages for anything everything), supports translation, etc. In the negatives however, 
you might be surprised to see something from the positives, the JavaScript ecosystem itself - there have been some notable issues over the years, such as 
[leftpad](https://en.wikipedia.org/wiki/Npm_left-pad_incident), [fakerjs](https://stackoverflow.com/a/70597188), malware, etc. Overall however it seems to be a good option, and was my 
second runner up option.

## So... Why Hugo?

So much text above, barely even mentioning Hugo - *sorry* - well now hopefully this will be helpful and justify and/or ease the pain of above :). Having looked at three options above, 
what boxes does Hugo tick, that are useful?

* [x] [Templates/Themes](https://themes.gohugo.io/) support, with a wide berth to choose from
* [x] The ability to easily expand functionality from the markdown text with [shortcodes](https://gohugo.io/shortcodes/)
* [x] [Translation](https://gohugo.io/content-management/multilingual/) support
* [x] Ability to tweak markdown rendering as needed via [hooks](https://gohugo.io/render-hooks/)
* [x] Compiles and runs fast, has a good dev experience
* [x] Community support: lots of plugins, easy to search for answers if needed, etc

Some quick negatives, are that while it supports translation, this effectively requires a "fork" of the content. However this isn't really a problem as it can be (hopefully) solved 
with external tooling, and is probably best left to it. Supporting the output of such tooling is fine.

In the ~~slightly~~, sorry, very subjective territory, Hugo makes it easy to [set up a project](https://gohugo.io/getting-started/quick-start/). From just needing Hugo itself, 
to the new project creation requiring a few commands, its such a breeze. In addition, when changes are made, all one has to do is run `hugo server` in the terminal, visit the URL 
in there browser, and on save content changes will be reflected. Plugins and templates are easily addable as submodules, meaning tooling such as 
[dependabot](https://github.blog/news-insights/product-news/keep-all-your-packages-up-to-date-with-dependabot/) can help you easily keep things up to date.

## Reflection

Its been a few months since we started using Hugo in the docs project. There have been some things that I wished it could do like support video in markdown, or markdown 
notices - but due to its great community, the first one was easy to solve with a shortcode, and the latter a plugin. I can't speak for everyone, but in my opinion it seems to 
have done its job and stayed out of the way. It seems that the lack of mention of things about Hugo, or problems related to it have been minimal at most, so I'll take that as a win.

