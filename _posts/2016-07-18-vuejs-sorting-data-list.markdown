---
published: true
title: vuejs sorting data list
layout: post
---
So i were trying to use [vue-sortable](http://sagalbot.github.io/vue-sortable/) with **v-for**. Fallowed setup guide and wolla - sortable list.

<script src="https://gist.github.com/revati/6a852ddc79de0adc386f85167e7e4487/cdac87ea93c9ab0bd522e269905ed44c77e491d5.js"></script>

DOM updates as it should, but i noticed that components data weren’t. So i googled and found [this](https://jsfiddle.net/peterburrell/rubagbc5/5/) and some [other](https://forum.vuejs.org/topic/888/best-way-to-keep-sortable-lists-in-order/4) similar approaches. Using DOM as source of truth? Isn’t it what vuejs, react and other reactive frameworks want to get rid of? And so much boilerplate code, doh.

Little bit playing around and it is easier than i thought...

<script src="https://gist.github.com/revati/6a852ddc79de0adc386f85167e7e4487.js"></script>

Nice :)