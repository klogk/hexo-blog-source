title: Hello World
date: 2015-01-08 19:43
---

之前用的是docpad。docpad生成静态文件速度太慢，乱七八糟的插件也太多了，过于臃肿。本来想迁移到jeklly，但苦于没怎么接触过ruby，如果要做一些个性化的定制就比较麻烦了。

偶然在知乎上看到有人推荐hexo，依然是用nodejs写的，特点就是简洁，编译的速度快，所以就试了试，看起来还不错，也就直接迁移过来了。

常见的命令有

### Create a new post

``` bash
$ hexo new "My New Post"
```
### Run server

``` bash
$ hexo server
```

### Generate static files

``` bash
$ hexo generate
```

### Deploy to remote sites

``` bash
$ hexo deploy
```

更多的可以参考官方网站 [hexo.io](http://hexo.io)

然后做了一些修改，主要是改模板，和增添latex的支持。 hexo和好几个模板都不支持。
