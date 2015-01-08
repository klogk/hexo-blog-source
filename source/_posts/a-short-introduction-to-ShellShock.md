---
title: ShellShock 漏洞(CVE-2014-6271)解析
layout: post
tags: ['public', 'post', 'web', 'it']
time: 2014-09-28 11:34
mathjax: false
---


在Bash中键入如下的命令

    env VAR='() { :;}; echo Bash is vulnerable!' bash -c "echo Bash Test"

如果你看到了如下的输出

	Bash is vulnerable!
	Bash Test

那么，恭喜你，你的Bash存在ShellShock漏洞。Bash 4.3以前的版本都存在这样的问题。解决的方法就是升级，ubuntu下面可以使用

    $ sudo apt-get update
    $ sudo apt-get install --only-upgrade bash

如果你只是为了了解如何修复这个漏洞，到这里就可以了。下面解析一下这个漏洞和攻击的原理。

###  ShellShock原理

看看一开始的这个命令，这个命令分为了两个部分。

后面是`bash -c "echo Bash Test"`，功能用bash执行后面的字符串中的命令，也就是把引号中的内容当成一个bash脚本来执行。

前面`env VAR='() { :;}; echo Bash is vulnerable!'`是定义了带有环境变量`VAR`的临时环境，放在最前面的语法含义是，在这个环境中执行后面的脚本。`env`一般还可以省略。也就等价于

    export VAR='() { :;}; echo Bash is vulnerable!'
    bash -c "echo Bash Test"

**注**：冒号`:`的含义是pass，也就是什么都不做。

大概就能够猜到， Bash把`VAR`定义中的内容当成了Shell命令来执行了。

的确如此，Bash可以把函数export到环境变量里面，就是把函数的代码当成了环境变量存下来的。尝试如下的命令

    export foo="() { echo hello; }"
    env | grep foo

输出如下

	foo=(){ echo hello; }

Bash把`foo`的函数体存在了环境变量里面。 执行foo

    foo

得到的输出是

    hello


Bash会先处理环境变量，看里面有没有函数定义。如果有，就把它执行成一个函数定义的命令。

当然，虽是函数，但如果不去调用它，那么依然是不会有问题的。

再看一个例子

    export foo='() { echo hello ; }; echo world'
    bash -c ''

执行上面的这两个命令会得到输出

    world

我们函数定义后面的内容意外的被执行了。所以，问题就在于Bash对于环境变量中的函数定义的转换是有漏洞的：它发环境变量函数中有函数之后，会把整个环境变量当做是一串Shell命令去执行。

**注**：在环境变量中定义函数的命令

    export foo="() { echo hello; }"

`()`后面和`{`之间的空格是必须的，否则Bash不会认为它是一个函数。

### CGI攻击

光是这样的漏洞，还不会造成什么危害。最容易受到攻击的原因，在于环境变量会和CGI联系起来。

简单举一个例子来解释CGI和环境变量的关系。即使没有了解过CGI，从这个代码中也能够明白个大概。

``` cpp
int main() {
	fprintf(stdout, "content-type: text/plain\n\n");
    char *method = getenv("REQUEST_METHOD");
    if(strncmp(method, "GET") == 0)
        fprintf(stdout, "input data is :\n%s", getenv("QUERY_STRING"));
}
```

上面的这个例子是一个C语言写的CGI。它处理一个GET请求，并把`query string`以plain text的方式输出。CGI中的stdout是进行管道重定向了，会作为Web服务器的响应，返回给客户端。

其中最关键的是两个`getenv`。在CGI的工作流程中，Web服务器会把http请求中的字段以环境变量形式传给CGI，例如`request method`、`query string`、`content length`、`content type`等等。

这样一来ShellShock漏洞就可能暴露到网络中。攻击者可以通过构造http请求，把上面的`echo`换成其它有攻击性或者泄露隐私信息的命令。例如

    wget -U "() { :;};echo \"Content-type: text/plain\"; echo; echo; /bin/cat /etc/passwd" http://***/test.cgi

`-U`就是设置`user agent`。 这样的一个请求就会把存在漏洞的机器上的 `/etc/passwd`文件暴露出来。

### 结束语

如果了解过SQL注入，就会发现ShellShock攻击和SQL注入是非常类似的，都是通过构造请求串， 来达到远程注入执行的目的。

除了CGI之外，还有其他的一些使用环境变量的服务器应用程序也可能会受到ShellShock的攻击。

例如，有人已经发现了可以用同样的思路去攻击qmail，http://weibo.com/1401527553/BoMzKgxPU?mod=weibotime。
