---
layout: post
title: "Python Unicode"
description: "UTF-8 with Json"
category: 
tags: []
---
{% include JB/setup %}
If the data structure in Python (e.g. dict, list) contains unicode, you must ensure this when dumping to json:
{% highlight python %}
import json
something_json = json.dumps(something_list, ensure_ascii=False, encoding='utf-8')
{% endhighlight %}
When you write the json string into the file like txt, you must ensure "utf-8" is on: 
```py
import codecs
with codecs.open(filename, "w", encoding="utf-8") as file:
    file.write(something_json)
```
  
This is no simple way of handling unicode in Python currently. 