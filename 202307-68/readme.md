啰里啰唆周刊第68期：泰森原则

本期对内容做了调整，取消了“一句话新闻”版块，于使内容更聚焦于科技和人文。

# 科技日常

## 1. Buildbot-基于python的开源持续构建和持续交付工具
Buildbot是python实现的开源持续构建和持续交付工具，为Python, Mozilla, Chromium, WebKit等知名项目使用。

Buildbot基于python网络框架Twisted，具备强大的扩展能力。带web-GUI，但是网页端管理能力比较弱，主要还是手写脚本和配置。
另外，对多项目支持也不佳。如果厌烦了Jenkins的，可以尝试换个口味。

[http://buildbot.net/](http://buildbot.net/)

## 2. Local-first software

> You own your data, in spite of the cloud。

这是一篇英语文章，讲的是本地优先策略，互联网得不可靠和易失性决定是不能完全依赖互联网。除此外，文章还列举了很多流行软件存在的问题，并介绍了一种local first并解决冲突的CRDT算法。

与前几代软件相比，当今的云应用提供了巨大的优势：无缝协作，并能够从任何设备访问数据。随着我们越来越多地通过这些云应用程序运行我们的生活和工作，它们对我们来说变得越来越重要。我们在使用这些应用程序之一上投入的时间越多，其中的数据对我们就越有价值。当数据存储在“其他人的计算机上”时，该第三方对该数据具有一定程度的控制。云应用作为服务提供;如果服务不可用，您将无法使用该软件，并且无法再访问使用该软件创建的数据。如果服务关闭，即使您可以导出数据，如果没有服务器，通常也无法继续运行该软件的自己的副本。因此，您受提供服务的公司摆布。

本地优先软件的七个理想
- No spinners: your work at your fingertips
- Your work is not trapped on one device
- The network is optional
- Seamless collaboration with your colleagues
- The Long Now
- Security and privacy by default
- Security and privacy by default

这篇文章篇幅很长，建议完整阅读全文。

[https://www.inkandswitch.com/local-first/](https://www.inkandswitch.com/local-first/)

## 3.1Panel-开源的 Linux 服务器运维管理面板
1Panel 是一个现代化、开源的 Linux 服务器运维管理面板，基于Golang开发。

1Panel 的功能和优势包括：

- 快速建站：深度集成 Wordpress 和 Halo，域名绑定、SSL 证书配置等一键搞定；
- 高效管理：通过 Web 端轻松管理 Linux 服务器，包括主机监控、文件管理、数据库管理、容器管理等；
- 安全可靠：基于容器来管理和部署应用，最小漏洞暴露面，提供防火墙和日志审计等功能；
- 一键备份：支持一键备份和恢复，备份数据到各类云端存储，永不丢失。

![](res/1p.png)

[https://github.com/1Panel-dev/1Panel](https://github.com/1Panel-dev/1Panel)

## 4.开源中文字体推荐 —— 霞鹜新致宋
霞鹜文楷的作者最近发布了新作品：霞鹜新致宋。

「霞鹜新致宋」是一款基于[「IPAmj 明朝」](https://moji.or.jp/mojikiban/font/)的中文开源字体，是将日本写法的字体改造成中国大陆规范写法的尝试，在「IPAmj 明朝」原有字形的基础上，将其改造成中国大陆规范字形。除此之外，重做了希腊字母和西里尔字母，与原字体拉丁字母部分风格基本一致，更适合现代希腊文及西里尔文的排版；新增对越南语拉丁字的显示支持。

符号方面，支持易经八卦和六十四卦符号、太玄经八十一卦符号、麻将符号、中国象棋符号、算筹数字、「正」字计数等特殊符号。

![](res/song.jpg)

目前该字体正在完善中，现提供「霞鹜新致宋」常用字测试版，包含 GB/T 2312-1980 一级字、《通用规范汉字表》一级字、《现代汉语常用字表》3500 字，此外也包含少量《通用规范汉字表》二、三级字。

[https://github.com/lxgw/LxgwNeoZhiSong](https://github.com/lxgw/LxgwNeoZhiSong)

## 5.Manticore Search -轻量级搜索引擎
Manticore Search 是一个使用 C++ 开发的高性能搜索引擎，创建于 2017 年，其前身是 Sphinx Search 。Manticore Search 充分利用了 Sphinx，显着改进了它的功能，修复了数百个错误，几乎完全重写了代码并保持开源。这一切使 Manticore Search 成为一个现代，快速，轻量级和功能齐全的数据库，具有出色的全文搜索功能。

Manticore Search目前在GitHub收获3.7k star，拥有大批忠实用户。同时开源者在GitHub介绍中明确说明了该项目是是Elasticsearch的良好替代品，在不久的将来就会取代ELK中的E。

来自 MS 官方的测试表明 Manticore Search 性能比 ElasticSearch 有质的提升。

[https://manticoresearch.com/](https://manticoresearch.com/)

# 读书与影视分享

## 1.2023韩国真人秀《海妖的呼唤：火之岛生存战》

韩国真人秀节目，邀请了军人、消防员、警察、警卫、运动员、特技演员六种职业的女性。然后按职业分成六个小组，让选手们在荒岛上生存。节目赛制都是实打实的，选手们不能靠撒娇找「村长」要糖吃，也没有人美心善的孩子愿意把好房子让出来。

优胜劣汰是这档综艺的底色。热血沸腾，帅气自信，有力量，好胜心和韧性满满的大女人们按职业分组，打基地攻防战。有联盟，有力量与智慧，有心理战，有同袍互助打气。刺探情报，布置陷阱，比拼战术。

![](res/haiyao.jpg)

> 韩综真的是已经另外一个世界了，我们还在玩泥巴。

> 相信我 这部综艺质量好到爆炸 形式内容都很创新 参考饥饿游戏 而且每个姐姐都有自己的闪光点 狠狠被女性力量治愈

## 2.美国电影《逃出克隆岛》
影片《逃出克隆岛》是2005年梦工厂出品的一部动作电影，由美国导演迈克尔·贝执导的一部科幻电影，伊万·麦克戈雷格、斯嘉丽·约翰逊等联袂出演，影片于2005年7月22日在美国上映。

影片的故事发生于21世纪中期，讲述了男青年林肯·6E生活在一个貌似乌托邦的社区里。梦想被选中成为“神秘岛”的访客，因为据说那个岛是这个星球上惟一没有被污染过的一片净土。但是不久后的一个意外让林肯惊觉：他其实是“神秘岛”居民们的克隆人，他的存在只是为了给他的“原型”提供各种更换用的身体零件。最后克隆人逃出囚笼、寻求真相的故事

> 陪室友重看了一遍，当初不理解为何此片媒体评论如此糟糕，如今多少明白了。前半段有着非常重的1984痕迹。
# 图论

## 1.Witty Animals

来自芝加哥的自由漫画家查克·英格沃森（Chuck Ingwersen）的系列作品俘获了许多人的心，并在艺术家的Instagram个人资料上为超过5万粉丝带来了微笑。

![](res/follow.jpg)

[ Instagram ](https://www.instagram.com/captainscratchy/)|[zazzle.com](https://www.zazzle.com/store/chuckink)
## 2.Continuous delivery tool landscape
James Bowman 在2017年绘制的一幅CI/CD工具链图，国内多有引用，但都打了各种水印，这里找到了原图出处,高清无码。

6年过去了，如果有更完善的landscape，可以留言反馈。

![](res/cd.jpeg)

[http://www.jamesbowman.me/post/continuous-delivery-tool-landscape/](http://www.jamesbowman.me/post/continuous-delivery-tool-landscape/)
# 谈天说地

## 1.Kid Cop Returns (Again and Again)
When Vincent Richardson was 14 years old, he wore a police uniform into Chicago’s Third District Grand Crossing police station and reported for duty. It was January 24th, 2009, and he told officers he’d been assigned by another district to work a shift there. An intake officer issued Vincent a police radio and ticket book; then, the officer assigned Vincent a partner and a police cruiser. 

Over the next five hours, they drove around the South Side of Chicago monitoring hot spots and responding to calls from dispatch. Vincent helped with traffic stops. He communicated with dispatchers using specific criminal codes about activities on the beat. He even assisted in an arrest helping to place handcuffs on someone suspected of violating a protective order.

> 十几岁时，文森特·理查森在成功冒充警察后成为芝加哥传奇人物。他被抓住了——那他为什么要一遍又一遍地这样做呢？好吧，当你真的很擅长某件事时...

[https://www.theverge.com/features/23737494/kid-cop-chicago-police-impersonator](https://www.theverge.com/features/23737494/kid-cop-chicago-police-impersonator)

## 2.凤凰是Phoenix吗
凤凰，又叫作“凤皇”，亦称凤鸟、丹鸟、火鸟、鶤鸡、威凤等，原型是五色锦鸡,为中国古代神话传说中的一对鸟类神兽组合，分有雌雄之别，雄为“凤”，雌为“凰”，合称为凤凰。据《山海经》记载，凤凰二鸟的形状像是普通的鸡，全身上下都是五彩斑斓的羽毛，头上的花纹是“德”字的形状，翅膀上的花纹是“羲”字的形状，背部的花纹是 “礼”字的形状，胸部的花纹是“仁”字的形状，腹部的花纹是“信”字的形状。

凤凰作为中国古代神话中的神兽，与神话故事中的龙一直都是最神秘的色彩,以至于不少的外国人也对于凤凰和龙都表示出极大的兴趣。凤凰的译名是“Phoenix”，而龙的译名则是“Dragon”，但其实这两个译名都是错误且广为流传的误译。

Phoenix 音译为菲尼克斯，它最大的特点就是重生，相传每隔五百年，Phoenix 就会采集各种有香味的树枝和草叶，叠成一堆再燃火自焚，然后变成灰烬，最后留下来的灰烬中会出现重生的幼鸟。所以大家也叫它重生鸟或不死鸟。其实不死鸟只是对一类特殊习性鸟类的一种误解。

凤凰和Phoenix 这两种根本不挨边的神鸟究竟是怎么扯上关系的？问题就出在“凤凰涅槃”这个著名的词上。这个词最早出处郭沫若先生写于1921年的同名诗作。郭先生将Phoenix 的能力强行加到凤凰身上，并自创了“凤凰涅槃”这一词。以至于在这之后，凤凰的译名就被正式的认定为是“Phoenix”，但其实凤凰的真正译名就应该是“FengHuang”，直接采用拼音形式。

> 黄永玉要写一个有关“凤凰涅槃”的文字根据，但一点材料也没有。《辞源》《辞海》《中华大辞典》《佛学大辞典》《人民日报》资料室，北京的民族学院、佛教协会都请教过了，没有！
忽然想起钱钟书先生，连忙挂了个电话，钱先生就在电话里说了以下的这些话：“这算什么根据？是郭沫若1921年自己编出来的一首诗的题目。三教九流之外的发明，你哪里找去？凤凰跳进火里再生的故事那是有的，古罗马钱币上有过浮雕纹样，也不是罗马的发明，可能是从希腊传过去的故事，说不定和埃及、中国都有点关系……这样吧！你去翻一翻大英百科……啊！不！你去翻翻中文本的简明不列颠百科全书，在第三本里可以找得到。”结果马上找到，解决了所有的问题。

> In China, the phoenix is called the businiao (不死鳥; literally "immortal bird"), whereas the fenghuang (鳳凰) is a mythical bird of local Chinese origin, similar to the phoenix. It is imagined as a composite of many birds, or even as comprising some body part of a snake, a fish etc. It is one of the most-respected legendary creatures in China and the feminine counterpart to the dragon. Its rare appearance is said to foreshadow a great event or bear testimony to the greatness of a ruler.

Dragon是西方神话中一种强大的生物，第一眼看上去外形类似一只长着类似蝙蝠肉翼的蜥蜴。龙有很多种，生活环境从沙漠到森林，甚至海洋都有分布，习性和颜色也随种类的不同而不同，共通的特点是喜欢财宝，穴居，会喷火。

中国“龙”则是中国历史上的一个图腾形象。在中国古代传说中，龙是一种能兴云降雨的神异动物。在封建时代，龙则作为皇帝的象征。现在中国龙的译名已经被认定为是“Loong”。

西方文化中，特性、含义、地位最接近中国的“龙”的概念就是“Seraphim”（炽天使），其原本的形象是“燃烧的大蛇”。所以用“Chinese Seraphim”来解释“Loong”是最合理可行的。因为西方文化中各方面本质含义和特性都最接近中国的“龙”的概念就是“Seraphim”（炽天使），不仅在西方神话宗教中的地位作用意义与“龙”在中国神话宗教中的地位作用意义最吻合，而且古希伯来语里“Seraphim”的词源意思就和中国龙的一种主要起源相同。

> 不涉及文化自信和专业著作的话，其实说凤凰就是Chinese Phoenix问题也不大，毕竟存在一定的历史渊源和众所周知的知名度。我个人觉得Phoenix更有气势，更有文化内涵。至于Chinese New Year和Lunar New Year则是一个掺和了政治的话题。

[https://en.wikipedia.org/wiki/Phoenix_(mythology)](https://en.wikipedia.org/wiki/Phoenix_(mythology))

## 3.泰森原则
这是一条会引发争吵的微博，但还是得发。
最近接连看到了几条新闻，都是关于幼儿在公共场合哭闹而引发矛盾的，比如国内高铁上有乘客之间因为孩子哭闹而互怼的，还有乘务员要求家长带孩子去车厢之间以免打搅其他乘客休息的，更夸张的在韩国，很多场所甚至打出了禁止儿童入内的告示，而这种措施还受到了不少人的欢迎。
我是完全主张在公共场合要包容幼儿及其家长的，这类事情的频发让我不由得想起微博上一位老师的话。

当时也是网上各种怪戾扯淡的事情频发，那位老师看到后就感慨，说当今社会上弥漫着一股“有今没明”的气氛，我当时就觉得这话太准了，有今没明说的再确切一些，就是人们普遍放弃了对长远未来的期待和规划，转而把注意力聚焦在短期的享乐和苟且上，任何与之相悖的事情都会引发人们的排斥。
我给个暴论，如今公共场合下对幼儿的责难和苛求，其实也是社会上“有今没明”气氛的体现，毕竟生养孩子是一个超长线的投资，需要付出无数的时间和心力，那完全是一种对长远未来的投资，和有今没明的心态是根本背离的，一个只在乎当下的人，自己不会做生养孩子的选择，也一样难以容忍别人的孩子给自己带来的麻烦，这在生育率普遍暴跌的中国和韩国，逻辑是一样的。

有人看到这该骂了，说你河森堡就是喜欢在道德高地上装逼，难不成儿童在公共场合闹的多过分我都得忍？

为了回应这个诘问，我给大家介绍一个“泰森原则”，所谓的泰森原则就是如果在公共场合，同样的麻烦不是一个小朋友搞出来的，而是拳王泰森搞出来的，你会不会忍？如果一个光头，脸上刺青，一身横肉，蹲过监狱，脾气暴躁且一拳就能让人断片的巨汉搞出了同样的动静，你选择忍耐，那换成小朋友，你也应该一样忍耐，如果那麻烦就算是泰森搞出来的你都忍不了，那你就可以抗议。

一个人若是在公共场合对泰森和小朋友持有不同的标准，那就说明他的抗议在公共道德之外还混杂了其他的东西。

我发这篇文章，就是在针对他们混进去的那些其他的东西。 

[@河森堡](https://weibo.com/u/5992829552)

## 4.科技数码自媒体的“MIUI困境”
我们都讨厌广告。

文章，视频，社交媒体…网络上美好的东西似乎基本上都是“免费”的。它像一个张开盖子的捕蝇草：色彩丰富，眼花缭乱，也许还有点臭臭的。我们自愿飞进去享受这一切，交出我们的注意力，并通过广告的形式，被具体的消化掉。

但这个过程总归不太舒服。绝大部分广告都构成一种对体验的破坏，B站因此做出了「不加贴片广告」的承诺。可问题依旧存在。一方面，收益下降，创作者“停更”，希望他们加回贴片的呼声不绝于耳。另一方面，当你在弹幕里看到“恰饭”两个字，如果没有直接退出，至少也会下意识地调低期待。

大家都很难受。

牺牲用户体验(这对自己也是一种伤害)来换钱，还是坚持日子难以为继的不变质？对B站和它的UP主而言，这都是个重大，而且长期无解的问题，也是这期节目的两位嘉宾日日面对的「行业现状」。所以面对B站即将(如果不是已经)到来的播放时长变革，我们希望坐下来，好好聊一聊这个死局，和这次变革中隐含的那点“希望的闪光”。

叔叔是认真的。B站确实“有可能倒闭，但绝不会变质”，我们找到了证据。

> 这是一篇播客，可在页面顶部点击收听。

[https://www.gcores.com/videos/167988](https://www.gcores.com/videos/167988)
# 联系方式

啰里啰唆是一份针对互联网和生活爱好者的数字杂志，旨在发现和分享一切有趣的东西。话题不固定，每期大约十五分钟阅读量，暂定每周四发布。部分内容来自互联网采编，如果为有来源的转载，均会注明转载地址或保留水印。

这是一个关注人文和科技的newsletter。

使用方法建议或素材提供

频道：notonlyshare

邮箱：auokyob@outlook.com

github地址：[https://github.com/iminto/luoliluosuo-weekly](https://github.com/iminto/luoliluosuo-weekly)