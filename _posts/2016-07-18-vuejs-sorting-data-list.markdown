---
published: true
title: vuejs sorting data list
layout: post
---
So i were trying to use [vue-sortable](http://sagalbot.github.io/vue-sortable/) with **v-for**. Fallowed setup guide and wolla - sortable list.

```
<template>
  <ul v-sortable>
    <li v-for="item in items"></li>
  </ul>
</template>
<script>
export default {
  data () {
    return {
      items: [1, 2, 3]
    }
}
</script>
<style>
</style>
```

DOM updates as it should, but i noticed that components data weren’t. So i googled and found [this](https://jsfiddle.net/peterburrell/rubagbc5/5/) and some [other](https://forum.vuejs.org/topic/888/best-way-to-keep-sortable-lists-in-order/4) similar approaches. Using DOM as source of truth? Isn’t it what vuejs, react and other reactive frameworks want to get rid of? And so much boilerplate code, doh.

Little bit playing around and it is easier than i thought...

```
<template>
  <ul v-sortable="{onEnd: reorder}">
    <li v-for="item in items"></li>
  </ul>
</template>
<script>
export default {
  data () {
    return {
      items: [1, 2, 3]
    }
  },
  methods: {
    reorder ({newIndex, oldIndex}) {
      this.items.splice(newIndex, 0, this.items.splice(oldIndex, 1)[0])
    }
  }
}
</script>
<style>
</style>
```

Nice. Vue component code highlighting also would be nice.