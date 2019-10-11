---
layout: page
title: About
description: 相信技术的力量
keywords: Piere Ming, sustar，微观漫步
comments: true
menu: 关于
permalink: /about/
---

我是皮尔斯-明，冲破一切束缚，换取美好明天。

我是微观漫步，我相信真正的美和浪漫存在于细微之处，我愿意与你一起去发现。

仰慕「设计的艺术」，便只好将编码作为工具，励志成为一个designer。

坚信熟能生巧，努力改变人生。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
