Apache HTTP server benchmarking tool

ab是一个用来基准评估(benchmarking)你的Apache HTTP服务器的工具。它针对你当前的Apache安装的性能表现给你提供一个直观概览，尤其是你的Apache安装每秒钟所能服务的请求数。

摘要

ab [ -A auth-username:password ] [ -b windowsize ] [ -B local-address ] [ -c concurrency ] [ -C cookie-name=value ] [ -d ] [ -e csv-file ] [ -f protocol ] [ -g gnuplot-file ] [ -h ] [ -H custom-header ] [ -i ] [ -k ] [ -l ] [ -m HTTP-method ] [ -n requests ] [ -p POST-file ] [ -P proxy-auth-username:password ] [ -q ] [ -r ] [ -s timeout ] [ -S ] [ -t timelimit ] [ -T content-type ] [ -u PUT-file ] [ -v verbosity] [ -V ] [ -w ] [ -x <table>-attributes ] [ -X proxy[:port] ] [ -y <tr>-attributes ] [ -z <td>-attributes ] [ -Z ciphersuite ] [http[s]://]hostname[:port]/path
选项

-A auth-username:password
向服务器提供基本的认证凭据。用户名与密码由一个冒号:分隔，并且经base64编码后发给服务器。无论服务器是否需要(即服务器是否已发来401未认证代码 - 401 Unauthorized)，此字符串都会被发送。

-b windowsize
TCP发送/接收缓冲区大小（字节数）。

-B local-address
当要建立向外的连接时所绑定的地址。

-c concurrency
一次性执行多个请求的数目。缺省是一次一个请求。

-C cookie-name=value
添加一个cookie：头行到请求中。该参数典型的是以一个名字/值对的形式name=value。该字段可重复。

-d
不显示"percentage served within XX [ms] table"。即结果中不显示一个表，该表会列出在XX毫秒内得到服务的请求占所有请求的百分比(遗留支持)。

-e csv-file
产生一个由逗号分隔值的(CSV)文件，其中包含了处理每个相应百分比请求(从1%到100%)所需时间(以微秒为单位)所占整个处理时间的百分比。这种格式比"gnuplot"文件更有用，因为后者其结果已经丢弃。

-f protocol
指明SSL/TLS协议(SSL2, SSL3, TLS1, TLS1.1, TLS1.2, or ALL)。TLS1.1和TLS1.2在2.4.4及以后版本仍有支持。

-g gnuplot-file
把所有测量结果值写入一个"gnuplot"或TSV(以Tab分隔)文件。此文件可以方便地导入到 Gnuplot, IDL, Mathematica, Igor或者Excel中。文件第一行为标签。

-h
显示使用方法信息。

-H custom-header
向请求附加额外的头信息。该参数典型是一个有效的头信息行的形式，其中包含了以冒号分隔的字段/值对(如："Accept-Encoding: zip/zop;8bit")。

-i
执行HEAD请求，而不是GET 。

-k
启用KeepAlive功能，即在同一个HTTP会话中执行多个请求。缺省KeepAlive功能不启用。

-l方法。在2.4.10及以后版本可用。
如果响应的长度不恒定，就不报告错误。该选项对于动态页可能有用。在2.4.7及以后版本可用。

-m HTTP-method
定制用于请求的HTTP方法。在2.4.10及以后版本可用。

-n requests
测试会话所要执行的请求个数。默认仅执行一个请求，通常会产生不具有代表性的基准测试结果。

-p POST-file
包含了要POST的数据的文件。记住还要设置-T选项。

-P proxy-auth-username:password
向中转代理提供基本认证信息。用户名和密码由一个冒号:隔开，并以base64编码形式发送。无论服务器是否需要(即服务器是否已发来407要求代理认证代码 - 407 Proxy Authentication Required)，此字符串都会被发送。

-q
当处理超过150个请求时，ab会在标准错误输出stderr中每隔10%或100条请求输出一个进度计数。使用该-q标记将屏蔽这些消息。

-r
当socket接收错误时，不退出。

-s timeout
在socket超时之前等待的最大秒数。缺省为30秒。在2.4.4及以后版本中可用。

-S
不显示中位值和标准方差值，当平均值和中位值超过标准差偏离1倍或2倍时，也不显示警告/错误信息。缺省会显示最小值/均值/最大值。(遗留支持)。

-t timelimit
用于基准测试的最大秒数。这内部隐含着-n 50000。使用该选项来在一个固定时间量内对服务器作基准测试。缺省无时间限制。

-T content-type
用于POST/PUT数据的Content-type头，例如application/x-www-form-urlencoded。缺省为text/plain。

-u PUT-file
包含要PUT的数据的文件。记住还要设置-T选项。

-v verbosity
设置信息显示的等级 - 4及以上会打印出头信息，3及以上会打印出响应代码（404,200，等等），2及以上会打印出警告和提示。

-V
显示版本号并退出。

-w
在HTML表中打印结果。缺省的，表为两列，白色背景。

-x <table>-attributes
用作HTML <table>标记的属性的字符串。属性被插入<table *这儿*>。

-X proxy[:port]
使用代理服务器用于请求。

-y <tr>-attributes
用作HTML <tr>标记的属性的字符串。

-z <td>-attributes
用作HTML <td>标记的属性的字符串。

-Z ciphersuite
指定SSL/TLS加密套件（见openssl加密器）。

输出描述

如下列表描述了ab的返回值：

Server Software
服务器软件。该值若有，就在第一个成功响应的服务器HTTP头中返回。其包括头中从开始直到检测到一个十进制值为32的字符（特别是：一个空格或者CR/LF）的所有字符。

Server Hostname
服务器主机名。命令行中给出的DNS或者IP地址。

Server Port
服务器段口号。ab所正连接的端口。如果在命令行中没有给出端口号，对于http就会缺省为80，对于https缺省为443。

SSL/TLS Protocol
SSL/TLS协议。该协议参数由客户端和服务器协商。只有当SSL协议被使用的时候才会打印出来。

Document Path
文档路径。从命令行字符串解析出来的请求URI。

Document Length
文档长度。第一个成功返回的文档的大小（字节数）。如果该文档长度在测试过程中发生了变化，响应会被认为出错。

Concurrency Level
并发等级。测试中使用的并发客户端的数目。

Time taken for tests
测试所用时间。从第一个socket连接建立到最后一个响应收到的时间。

Complete requests
完成的请求。收到的成功响应的数目。

Failed requests
失败的请求。被考虑为失败的请求的数目。如果该值大于0，另一行将被打印出来以列出由于连接，读取，不正确的内容长度或者例外导致失败的请求的数目。

Write errors
写错误。在写的时候（broken pipe）失败的错误数。

Non-2xx responses
非2xx响应数。响应码不是200系列的响应的数目。如果所有响应都是200，该字段不会被打印出来。

Keep-Alive requests
导致Keep-Alive请求的连接数。

Total body sent
如果配置了发送数据作为测试的一部分，这就是测试中所发送的总字节数。如果测试没有包括一个body来发送，该字段就忽略掉。

Total transferred
总传输字节数。从服务器收到的总字节数。该数值本质上是线路上发送的字节数。

HTML transferred
总传输文档字节数。从服务器收到的文档字节总数。该数值排除了收到的在HTTP头中的字节数。

Requests per second
每秒请求数。该值是所有请求数除以所耗时间获得。

Time per request
平均每请求所花时间。输出结果中会显示两行该值，第一个值由公式concurrency * timetaken * 1000 / done计算得到，而第二个值由公式timetaken * 1000 / done计算得到。就是说第一个值是排除并发因素对平均时间的减少，结果就是服务器、网络完全单一串行对请求的处理能力（所花费的每请求平均时间），第二个值则借助并发实现了平均每请求所花时间的减少。

Transfer rate
传输速率。由公式totalread / 1024 / timetaken计算得到。

简单实例
<div class="highlight highlight-source-lisp"><pre>3y2y@ubuntu:~$ ab -A 3y2y:<span class="pl-c1">12345678</span> -c <span class="pl-c1">20</span> -n <span class="pl-c1">200</span> http://www.3y2y.com/test.php
This is ApacheBench, Version <span class="pl-c1">2.3</span> &lt;$Revision: <span class="pl-c1">1528965</span> $&gt;
Copyright <span class="pl-c1">1996</span> Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking yingtrader.pusunny.com (be patient)
Completed <span class="pl-c1">100</span> requests
Completed <span class="pl-c1">200</span> requests
Finished <span class="pl-c1">200</span> requests


Server Software:        Apache/<span class="pl-c1">2.4.7</span>
Server Hostname:        www.3y2y.com
Server Port:            <span class="pl-c1">80</span>

Document Path:          /test.php
Document Length:        <span class="pl-c1">145609</span> bytes

Concurrency Level:      <span class="pl-c1">20</span>
Time taken for tests:   <span class="pl-c1">26.670</span> seconds
Complete requests:      <span class="pl-c1">200</span>
Failed requests:        <span class="pl-c1">0</span>
Total transferred:      <span class="pl-c1">29198800</span> bytes
HTML transferred:       <span class="pl-c1">29121800</span> bytes
Requests per second:    <span class="pl-c1">7.50</span> [<span class="pl-c1">#/sec</span>] (mean)
Time per request:       <span class="pl-c1">2666.952</span> [ms] (mean)
Time per request:       <span class="pl-c1">133.348</span> [ms] (mean, across all concurrent requests)
Transfer rate:          <span class="pl-c1">1069.18</span> [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       <span class="pl-c1">55</span>  <span class="pl-c1">341</span> <span class="pl-c1">154.0</span>    <span class="pl-c1">306</span>     <span class="pl-c1">639</span>
Processing:  <span class="pl-c1">1216</span> <span class="pl-c1">2252</span> <span class="pl-c1">357.9</span>   <span class="pl-c1">2303</span>    <span class="pl-c1">3464</span>
Waiting:       <span class="pl-c1">53</span>  <span class="pl-c1">486</span> <span class="pl-c1">313.1</span>    <span class="pl-c1">403</span>    <span class="pl-c1">1750</span>
Total:       <span class="pl-c1">1273</span> <span class="pl-c1">2594</span> <span class="pl-c1">358.9</span>   <span class="pl-c1">2649</span>    <span class="pl-c1">3612</span>

Percentage of the requests served within a certain time (ms)
  <span class="pl-c1">50</span>%   <span class="pl-c1">2649</span>
  <span class="pl-c1">66</span>%   <span class="pl-c1">2693</span>
  <span class="pl-c1">75</span>%   <span class="pl-c1">2712</span>
  <span class="pl-c1">80</span>%   <span class="pl-c1">2743</span>
  <span class="pl-c1">90</span>%   <span class="pl-c1">2762</span>
  <span class="pl-c1">95</span>%   <span class="pl-c1">3118</span>
  <span class="pl-c1">98</span>%   <span class="pl-c1">3230</span>
  <span class="pl-c1">99</span>%   <span class="pl-c1">3400</span>
 <span class="pl-c1">100</span>%   <span class="pl-c1">3612</span> (longest request)</pre></div>
