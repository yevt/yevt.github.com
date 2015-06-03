---
layout: post
title: "xhr doesn't work with file protocol"
description: "XMLHttpRequest GET can't load urls like file://path-to-file"
category: programming
tags: [js, xhr, file]
---
{% include JB/setup %}

Файловая струкрура:

![/static/img/Screen Shot 2015-06-03 at 10.59.54.png](/static/img/Screen Shot 2015-06-03 at 10.59.54.png)

Код **index.html**

{% highlight js %}

var xhr = new XMLHttpRequest();
xhr.open("GET", "file.json", true);
xhr.onreadystatechange = function() {
    var status;
    if (xhr.readyState == 4) { // `DONE`
        status = xhr.status;
        if (status == 200) {
            console.log(xhr.responseText);
        } else {
            throw {message: "Could not load file"};
        }
    }
};
xhr.send();

{% endhighlight %}

Файл **file.json** не загрузится если открыть **index.html** в браузере без веб сервера.

[Скриншот](/static/img/Screen Shot 2015-06-03 at 10.39.20.png)

Если загрузить этот же **index.html** по http-протоколу, то **file.json** загрузится.

[Архив с проектом](/static/other/xhr-with-file-protocol-doesn_t-work.zip)