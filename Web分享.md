目录：
* Web资源 --- URI URL URN 资源传输
* API --- 原因 应用 操作资源
* 网络 因特网 互联网 万维网
 
## Web资源
早期 Web资源：在网络中有地址的静态文件  
现在 Web资源：可以被识别、被命名、或被处理的任何实体  
资源的形式多种多样，文档、图片、音乐、电影、数据库、网页、服务都可以算作是资源  
互联网上这么多资源，怎么区分，怎么找到我想要的资源呢？这就需要用到URI(统一资源标志符) 

### URI 统一资源标志符
URI是一个用于标识某一互联网资源名称的字符串。每个资源的URI是独一无二的，这样才能把它们区分开。  
例如：   
1. http://www.w3school.com.cn/tags/index.asp 代表W3school网站上的一份参考手册 
2. sftp://67.216.199.87:26894/ 代表我VPS上的ssh服务  
3. thunder://QUFlZDJrOi8vfGZpbGV8JTVCJUU4JUJGJTg1JUU5rOi8vfGZpb...... 代表迅雷服务器上的一部电影 
4. magnet:?xt=urn:btih:AC55FAEAE28DD449F19130961DA3646E7ABA324D 磁力链接，代表一个资源 

### URL URN 与 URI
URL是统一资源定位符，对可以从互联网上得到的资源的位置和访问方法的一种简洁的表示，是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的URL，它包含的信息指出文件的位置以及浏览器应该怎么处理它。  

URN是统一资源名称。可以表示唯一的资源，但是不能给出实体的位置。系统可以先在本地寻找一个实体，在它试着在Web上找到该实体之前。它也允许Web位置改变，然而这个实体却还是能够被找到。  

URI包括URL和URN。上面例子中的(1)(2)是URL，因为其中有路径可以确定资源的位置，这样才能找到它。上面例子中的(3)(4)是URN，因为它带有文件的特征码，表示了文件独一无二的身份。   

下面引用知乎的回答进一步解释这些概念  
[HTTP 协议中 URI 和 URL 有什么区别？](https://www.zhihu.com/question/21950864)

### Web资源的传输
在了解Web资源的概念之后，我们知道了URI可以区分不同的资源，根据URI我们就可以找到指定的资源。但还有一个问题，这些Web资源储存在服务器上，它们是怎么传输到我们的电脑上呢？换句话说，当我们请求一个资源时，真实的物理世界发生了哪些事？我们想知道信息是如何传递的？它经过了哪些线路？  
[How Does the Internet Work?](https://www.youtube.com/watch?v=ewrBalT_eBM&t=72s)

## API
API（Application Programming Interface,应用程序编程接口）是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。API本身是抽象的，它仅定义了一个接口，而不涉及应用程序在实际实现过程中的具体操作。  
从形式的角度看：  
API像函数声明一样，指定了参数和返回结果，负责一个程序和其他软件的沟通，本质是预先定义的函数。  
从设计的角度看：  
把某些功能封装好，方便其他人调用。调用的人可以很方便使用这些功能，并且可以不需要知道这些功能的具体实现过程。  

### 为什么使用API
程序之间是互相联系的，它们彼此依赖，需要协调配合等才能完成任务。API的目的就是把这种通讯方式事先约定好，当请求方调用API时，接收方负责实现具体过程。这么一来，请求方只需调用API，不用知道具体操作就能完成任务。

### API的应用
下面看一些具体的应用情景  
1. 操作系统API  
比如你想做一个单机游戏的修改器，修改玩家的生命值。尽管你知道游戏中生命值对应的内存地址，但是修改器和游戏是两个不同的进程，你不能直接修改这个内存。怎么办？我们知道操作系统可以管理计算机硬件与软件资源，它是有权限修改内存的。所以就我们请求操作系统修改内存，这就需要调用操作系统的API。  
操作系统留给应用程序的一个调用接口，应用程序通过调用操作系统的API而使操作系统去执行应用程序的命令。 

2. 多媒体API  
DirectX是由微软公司创建的多媒体编程接口。由C++编程语言实现，遵循COM。被广泛使用于Microsoft Windows、Microsoft XBOX、Microsoft XBOX 360和Microsoft XBOX ONE电子游戏开发，并且只能支持这些平台。最新版本为DirectX 12，创建在最新的Windows10。  
DirectX API 帮助游戏开发者设计炫酷的画面，而不必在意显卡是如何工作的。  

3. Web API  
什么是Web API呢？  
如果我们想要获取一篇Blog，输入http://localhost:9000/blog/123 ，就可以看到id为123的Blog页面，但这个结果是HTML页面，它同时混合包含了Blog的数据和Blog的展示两个部分。对于用户来说，阅读起来没有问题，但是，如果机器读取，就很难从HTML中解析出Blog的数据。  
如果一个URL返回的不是HTML，而是机器能直接解析的数据，这个URL就可以看成是一个Web API。比如，读取http://localhost:9000/api/blogs/123 ，如果能直接返回Blog的数据，那么机器就可以直接读取。  
REST就是一种设计API的模式。最常用的数据格式是JSON。由于JSON能直接被JavaScript读取，所以，以JSON格式编写的REST风格的API具有简单、易读、易用的特点。   
编写API有什么好处呢？  
由于API就是把Web App的功能全部封装了，所以，通过API操作数据，可以极大地把前端和后端的代码隔离，使得后端代码易于测试，前端代码编写更简单。  

### Web中的API与资源
服务器上储存了很多各种各样的资源，其中一部分是对外开放的。如果用户随意的读取、修改、删除资源，这就很危险了。所以，对于外部的请求，我们总是使用API来操作服务器上的数据。使用API好处很多，第一：对请求做出了限制，保证了服务器数据的安全。第二：制定了一套规范，便于开发。  
下面举一些例子来说明API是如何操作资源的。 

V2EX是一个知名技术创意网站，由设计师、程序员及有创意的人参与的社区。它基于兴趣将用户创建的内容组织分类成不同“节点”，网站以内容的活跃程度决定在首页排序的位置。  
我们来看看这个网站的API [V2EX API](https://github.com/djyde/V2EX-API)  
>实验：用POSTMAN发出API请求，测试结果

推荐视频 [What is an API](https://www.youtube.com/watch?v=s7wmiS2mSXY)

## 关于网络（补充）
上面谈到的大部分内容都和Web有关。那么，Web到底是什么？  为了弄清楚这个问题，我们先要搞懂下面这些关键词。  
关键词：
1. 互联网(internet;internetwork;internection network)
2. 因特网(Internet)
3. 万维网(WWW;world wide web;Web)
4. HTTP(HyperText Transfer Protocol)
5. HTML(HyperText Markup Language)

网络：由若干结点和连接这些结点的链路组成。  
互联网：是网络的网络，是所有类型网络的母集。  
因特网：世界上最大的互联网网络。即 因特网概念从属于互联网概念。习惯上，大家把连接在因特网上的计算机都称为主机。  
万维网：万维网是一个大规模的、联机式的信息贮藏所，英文简称web。 特点是基于HTTP、HTML技术。简单理解是与“浏览网页”相关的网络系统。

Web（World Wide Web）即全球广域网，也称为万维网，它是一种基于超文本和HTTP的、全球性的、动态交互的、跨平台的分布式图形信息系统。是建立在Internet上的一种网络服务，为浏览者在Internet上查找和浏览信息提供了图形化的、易于访问的直观界面，其中的文档及超级链接将Internet上的信息节点组织成一个互为关联的网状结构。  
万维网用链接的方法能非常方便地从因特网上的一个站点访问另一个站点（超链技术），具有提供分布式服务的特点。万维网是一个分布式的超媒体系统，是超文本系统的扩充。万维网基于B/S架构工作。     
[Web 万维网](https://baike.baidu.com/item/Web/150564#2)


HTTP：为解决“用什么样的协议来实现整个因特网上的万维网文档”这一难题，就要使万维网客户程序（以浏览器为主，但不限于浏览器）与万维网服务器程序之间的交互遵守严格的协议，这就是超文本传送协议（HyperText Transfer Protocol）。HTTP是处于应用层的协议，使用TCP传输层协议进行可靠的传送。因此，需要特别提醒的是，万维网是基于因特网的一种广泛因特网应用系统，且万维网采用的是HTTP（端口：80）/HTTPS（端口：43）的传输协议，但因特网还有其他的网络应用系统（如：FTP、SMTP等等）。 

HTML：为了解决“怎样使不同作者创作的不同风格的万维网文档，都能在因特网上的各种主机上显示出来，同时使用户清楚地知道在什么地方存在着链接”这一问题，万维网使用超文本标记语言（HyperText Markup Language），使得万维网页面的设计者可以很方便地用链接从页面的某处链接到因特网的任何一个万维网页面，并且能够在自己的主机品目上将这些页面显示出来。HTML与txt一样，仅仅是是一种文档，不同之处在于，这种文档专供于浏览器上为浏览器用户提供统一的界面呈现的统一规约。且具备结构化的特征，这是txt所不具备的强制规定。  

## 部分参考资料
https://en.wikipedia.org/wiki/Web_resource  
https://www.zhihu.com/question/21950864  
https://baike.baidu.com/item/url/110640?fr=aladdin  
https://baike.baidu.com/item/URN  
https://www.zhihu.com/question/38594466  
https://zh.wikipedia.org/wiki/%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E6%8E%A5%E5%8F%A3  
https://www.youtube.com/watch?v=s7wmiS2mSXY  
https://www.zhihu.com/question/19860216  
https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001402402473485d8c205b735ee4e698f90769960fcec4b000  
https://www.zhihu.com/question/58274241  
https://github.com/djyde/V2EX-API  
https://www.douban.com/note/323728072/  
https://baike.baidu.com/item/Web/150564  
https://www.zhihu.com/question/19860216  
https://www.zhihu.com/question/20597473  
