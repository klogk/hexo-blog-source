---
title: Docpad-plugin-pygments configuration 
layout: post
tags: ['public', 'post', 'docpad', 'pygments']
time: 2013-05-25 12:00
---

[Docpad-plugin-pygments](https://github.com/docpad/docpad-plugin-pygments) is a plugin of docpad using pygments. [Pygments](http://pygments.org/download/) is a generic syntax highlighter implemented in Python.

When I use docpad to setup this website, I found the configuration is more than using `npm install`. So I want to record those steps here.

All the following steps are performed in the top directory of docpad site.

- Install pygments.

```
sudo apt-get install python-setuptools
sudo apt-get install python-pip
sudo pip install pygments
```

- `npm install` docpad-plugin-pygments. 

In the directory of docpad, execute following command

```
npm install docpad-plugin-pygments
```

- Download `pygments-default.css`. 

Put it into the source directory `src/documents/styles/`.

```
mv pygments-default.css src/documents/styles/pygments-default.css
```
Modify `docpad.coffee`, add `/styles/pygments-default.css` into the list of `styles`.

- Modify `pygments.plugin.js`.

Edit `node_modules/docpad-plugin-pygments/out/pygments.plugin.js` with following modifications.

a) Add options for highlighted code generation. Modify the array `command`

``` javascript
command = ['-f', 'html', '-O', 'style=colorful,linenos=inline,encoding=utf-8'];
```
This command options add `colorful` style and line number.

b) Insert code to decode HTML escape character before `pygmentizeSource(source, language, function(err, result){...})`

``` javascript
function htmlDecode(str){
    var s = "";
    if (str.length == 0) return "";
    s = str.replace(/&amp;/g, "&");
    s = s.replace(/&lt;/g, "<");
    s = s.replace(/&gt;/g, ">");
    s = s.replace(/&#39;/g, "\'");
    s = s.replace(/&quot;/g, "\"");
    return s;
};
source = htmlDecode(source);
```

c) Disable code indentation remove. 

Modify `source = balUtil.removeIndentation(bottomNode.innerHTML);` to

``` javascript
//source = balUtil.removeIndentation(bottomNode.innerHTML);
source = bottomNode.innerHTML;
```

After these steps, `docpad-plugin-pygments` is working properly.
