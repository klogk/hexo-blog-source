---
title: 基于Google API + SAE的Contest Calendar 
layout: post
tags: ['public', 'post', 'Google API','SAE', 'contest', 'calendar']
time: 2011-05-28 20:35
---

昨天，突然有个想法，想做个Contest Calendar，有的网站上已经也有这个功能。不过我感觉不太方便用，每次都要去查页面。如果能够做成直接把Contest的信息集成到Google Calendar中，这样就可以增加alert，还可以和朋友直接分享，多好。

Google Data API中有一个Google Calendar API，提供了对Google Calendar操作的接口。Sina App engine提供了一个云计算平台，正好可以用用。

## 比赛信息数据
为了偷懒，先直接从某个现成的网站上抓吧，哈哈。

无论是抓取网页，还是后面调用Google Calendar API，都需要用到PHP的cURL库。cURL库类似于Linux下面的curl命令，可以进行网络数据的传送。

cURL的使用，分3步

第一步，初始化，得到一个cURL句柄。

``` php
$curl=curl_init();
```

第二步，设置请求信息。包括URL地址，Header，传送的数据(POST方式)等等。我用到的有如下一些。

``` php
curl_setopt($_curl, CURLOPT_URL, $url); // the url to fetch
curl_setopt($_curl, CURLOPT_POST, 1);   // using POST method
curl_setopt($_curl, CURLOPT_HEADER, true);   // sending HEADER 
curl_setopt($_curl, CURLOPT_POSTFIELDS, $data); // the data to POST
curl_setopt($_curl, CURLOPT_HTTPHEADER, $header); // the content of HEADER
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true); // true to return the result. otherwise the data will be output directly
```

第三步，执行curl。

```php
$res=curl_exec($curl);
```

一般都要在上一步设置CURLOPT_RETURNTRANSFER为true，然后用返回的数组去处理。$res就是目标URL返回的信息，默认情况下是网页HTML数据。

此外，可以检查curl执行的有关信息

``` php
$info = curl_getinfo($curl);
```

$info的结构如下

``` php
(
    [url] => https://www.google.com/calendar/feeds/default/private/full?alt=jsonc&gsessionid=JHw5wBR9Nx2j0UURXGK3-Q
    [content_type] => application/json; charset=UTF-8
    [http_code] => 500
    [header_size] => 361
    [request_size] => 1004
    [filetime] => -1
    [ssl_verify_result] => 0
    [redirect_count] => 0
    [total_time] => 0.591147
    [namelookup_time] => 1.3E-5
    [connect_time] => 0.000477
    [pretransfer_time] => 0.000509
    [size_upload] => 0
    [size_download] => 139
    [speed_download] => 235
    [speed_upload] => 0
    [download_content_length] => 925
    [upload_content_length] => 0
    [starttransfer_time] => 0.591125
    [redirect_time] => 0
)
```

更多关于cURL的资料可以查看[1][2]。

我先用cURL抓取了南开大学OJ上的一个contest list(http://acm.nankai.edu.cn/recent_contests.php )。接下来处理HTML数据时候遇到点小麻烦，sae禁止使用DOMDocument，很囧。我只好自己用正则表达式来做。

南开OJ上的这个列表，是放在一个table里面的，只需要提取出<td>…</td>中的内容就好了。我使用的pattern是

``` php
$pattern='|<td([^>]*)>(.*)</td>|U';
```

简单解释下

1．*和形式语言理论中的意思一样，表示前面的字符或者部分重复0次以上
2．小数点表示任意字符
3．^号如果出现在中间，表示不含后面的字符
4．中括号表示字符集合，相当于形式语言里面论的大括号，里面的字符都取且只取一个。
5．小括号是为了后面匹配用的。

正则表达式更多的内容见[3]

构造pattern，接下来就是匹配了。可以使用了全局匹配函数preg_match_all来匹配，语法是

``` php
int preg_match_all($pattern,$text,$result [,OPTION]);
``` 

函数返回值是匹配的次数。

$result返回的是一个2维数组。$result[0]是匹配$pattern的所有子串组成的数组。$result[1]以及下标大于1的元素是第i个小括号匹配的子串，也就是要提取的`<td></td>`中的串。

结合$result再进行字符串处理，就能够得到比赛的名称、地址、时间信息。

## Google Calendar API
和一般的API一样，分成两步:

首先认证，得到Authorization Token

Google Data API提供了多种的Auth方式，包括OAuth for web/installed applications、AuthSub for web applications、ClientLogin for installed applications和Magic cookie authentication。

OAuth是现在微博、SNS用得比较多的方式。ClientLogin就是常见的用户名+密码的方式。我这个应用直接用ClientLogin。流程如下



图表 1 The ClientLogin authorization process(http://code.google.com/apis/accounts/docs/AuthForInstalledApps.html)

ClientLogin的步骤很简单。分两步，第一步读取用户名密码，第二步把用户名和密码发给Google Authorization service，然后就能够收到Google Authorization service返回的Token。某些时候可能需要验证码，就会再多一次交互的过程，就是途中绿色箭头的部分。然后用这个Token就可以使用API了。使用API时候，需要在每次请求的时候，在Http请求中增加如下的Header信息：

```
Authorization: GoogleLogin auth= DQ…KXZie
```

auth=后面的就是得到的Token

然后就可以使用Google Calendar API来创建event了。

首先，先在Google Calendar中创建一个新的日历，在日历设置中找到这个日历的设置，里面有一个Calendar ID，这是Google Calendar API识别是对哪一个日历操作的标识。



图表 2 Calendar ID

然后，构造请求数据。Google Calendar API可以使用两种方式来传送数据，一种是Atom，一种是JSON-C。我使用了JSON-C。

PHP中提供了处理JSON-C的函数 `json_encode` 和 `json_decode`

用于实现PHP类对象到JSON格式的编码，和从JSON格式到PHP 类对象的解码。以下就是Google Calendar API所使用的JSON格式示例

``` javascript
{
     "apiVersion": "2.3"
     "data": {
        "title": "Tennis with Beth",
        "details": "Meet for a quick lesson.",
        "transparency": "opaque",
        "status": "confirmed",
        "location": "Rolling Lawn Courts",
        "when": [
         {
            "start": "2010-04-17T15:00:00.000Z"
            "start": "2010-04-17T15:00:00.000Z"
         }
        ]
     }
}
```

其对应的PHP 类对象结构如下

```
stdClass Object
(
    [data] => stdClass Object
    (
        [title] => FZU
        [details] => 2011%C4%EA%C8%AB%B9%FA%B4%F3%D1%A7%C9%FA%B3%CC%D0%F2%C9%E8%BC%C6%D1%FB%C7%EB%C8%FC%A3%A8%B8%A3%D6%DD%A3%A9
        [when] => Array
        (
            [0] => stdClass Object
            (
                [start] => 2011-05-28 13:00:00+08:00
                [end] => 2011-05-28 13:00:00+08:00
            )
        )
        [location] => http://acm.fzu.edu.cn/contest/index.php?cid=115
    )
)
```

另外要注意一点，json_encode和json_decode是对unicode编码的字符进行转换。如果处理的JSON数据或者PHP类对象中有中文，要使用urlencode把中文进行编码。

构造好上面的数据后，把数据POST到如下地址

```
https://www.google.com/calendar/feeds/calendar-ID/private/full?alt=jsonc
```

要把calendar-ID换成上面得到的ID。做到这一步的时候，执行curl发送请求后，会返回302错误。

返回的数据HTML是这样的

```
HTTP/1.1 302 Moved Temporarily
Server: nginx/0.6.31
Date: Sat, 28 May 2011 08:53:14 GMT
Content-Type: text/html; charset=UTF-8
Transfer-Encoding: chunked
Connection: close
Expires: Sat, 28 May 2011 08:53:14 GMT
Set-Cookie: S=calendar=JHw5wBR9Nx2j0UURXGK3-Q;Expires=Sun, 27-May-2012 08:53:14 GMT;Secure
Location: https://www.google.com/calendar/feeds/calendar-ID /private/full?alt=jsonc&gsessionid=JHw5wBR9Nx2j0UURXGK3-Q
Cache-Control: private, max-age=0
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
...

```

Curl info中的内容是这样的

``` php
Array
(
    [url] => https://www.google.com/calendar/feeds/hk2ie6lsgllif5np45cgqutl9c@group.calendar.google.com/private/full?alt=jsonc&gsessionid=JHw5wBR9Nx2j0UURXGK3-Q
    [content_type] => application/json; charset=UTF-8
    [http_code] => 500
    [header_size] => 361
    [request_size] => 1004
    [filetime] => -1
    [ssl_verify_result] => 0
    [redirect_count] => 0
    [total_time] => 0.591147
    [namelookup_time] => 1.3E-5
    [connect_time] => 0.000477
    [pretransfer_time] => 0.000509
    [size_upload] => 0
    [size_download] => 139
    [speed_download] => 235
    [speed_upload] => 0
    [download_content_length] => 925
    [upload_content_length] => 0
    [starttransfer_time] => 0.591125
    [redirect_time] => 0
)
```

这是Google Calendar API中有这样一个机制，需要重新再POST一次。在第一次POST返回的url中提供了一个gsessionid和一个名为S的cookie。这些值是一样的，可以从返回页面响应得到，也可以从curl info中获取。

重新进行一次POST，这就需要在url后增加gsessionid参数，或者增加一个S cookie。这时候返回的信息如果包含create字样就表明是创建好了一个事件。

目前还在调整，Sina App Engine感觉不给力，经常出现Gateway Time-Out。再调试调试，就可以publish出去了，哈哈。

当然，也有封装好的Google Calendar API SDK，比如Zend Framework[5]提供了一个Google Data API SDK，但是其中使用了某些不被Sina App Engine支持的PHP函数，不能够直接移植过来。

## Reference

1. http://www.php.net/manual/en/function.curl-setopt.php

2. http://php.chinaunix.net/manual/zh/function.curl-setopt.php

3. http://php.net/manual/en/book.pcre.php

4. http://code.google.com/apis/calendar/

5. http://framework.zend.com/svn/framework/standard/trunk/demos/Zend/Gdata/Calendar.php
