啰里啰唆周刊第52期：看飞机的人

# 科技日常

## 1. 利用德摩根定律简化布尔运算
这两天在重构一些老项目，重构过程中遇到了一个让人非常头大的逻辑判断：
```java
if(!((A && B) || C)) {
  // do something
} else {
  // do something
}
```
看了这段代码，我人都傻了，从里向外一层一层梳理逻辑时，我的大脑活动是这样的：
![](res/brain.jpg)

短短一行的逻辑判断里，与或非三个运算符都用上了，尤其是最后那个小括号一圈全体取反的操作，我脑子直接炸了。要知道人脑是很不擅长或运算和非运算的，更不要说这些运算组合在一起了。

又花了五分钟尝试从代码上下文中梳理业务逻辑无果后，我重新审视了这个问题：如果业务上不好处理这个问题，能不能从理论上找到突破口？
方向找对后，我很快就找到了解决方案，那就是离散数学里的[德摩根定律（De Morgan's laws）](https://en.wikipedia.org/wiki/De_Morgan%27s_laws)。

ref:[https://supercodepower.com/De-Morgan-laws](https://supercodepower.com/De-Morgan-laws)
## 2. 小众软件-Midica 音乐编程软件
Midica is an interpreter for a Music Programming Language. It translates source code to MIDI.

But it can also be used as a MIDI Player, MIDI compiler or decompiler, Karaoke Player, ALDA Player, ABC Player, LilyPond Player or a MIDI File Analyzer.

You write music with one of the supported languages (MidicaPL, ALDA or ABC).

简单来说，就是把用代码生成MIDI文件。也支持对MIDI的编辑。

![](res/player.png)

官网：[http://www.midica.org/#](http://www.midica.org/)

## 3.AuroraStore - 开源第三方Google Play商店
Aurora Store是一款开源高速第三方Google Play商店。其前身是Yalp Store，Yalp Store 利用 Play Store 的非官方接口实现了无帐号下载应用。Yalp Store 停更后，Aurora Store 便拿起了接力棒。

使用 Aurora 可以下载应用程序、更新现有应用、搜索应用等。您还可以伪装您的设备信息、语言和区域，以访问您所在国家/地区或设备中尚未提供或受限的应用。
Aurora商店的运行不需要谷歌Play框架或Micro G组件，和Google PlayStore一样遵循Material Design而设计。

尽管 Aurora Store 本身无需 Google 服务，但从中下载的应用仍有可能依赖于 Google 套件。因此软件也友好地注明了软件的运行是否需要 Google Services 及软件内置的各类跟踪服务。若你想要使用那些含有内购、需要 Google 账号登录的软件或者游戏，那么 Google 服务仍然是必需品。

另外， Aurora 只能下载 Play Store 里面的免费软件，付费软件则需要通过 Web 端应用商店购买后登录下载。

该App需要连接到国际互联网。

[https://auroraoss.com/](https://auroraoss.com/)

## 4.localsend和sharik-AirDrop 的开源替代方案
可以通过本地网络与附近的设备，安全地共享文件和消息，此过程不需要互联网，不需要外部服务器，支持 Windows、Linux、macOS、Android、iOS 设备。

原理还是在同一个局域网内开一个HTTP服务器，如果要即支持局域网内共享，又要支持互联网共享，曾经有一款软件Send Anywhere支持，也有一些小众软件支持，但是目前大多不再维护了，因为跨网传输需要一个中转服务器，这需要一个不小的维护成本。

有很多场景，哪怕设备近在咫尺，却不能在同一个网络里，比如公司的办公电脑和手机之间，排除使用张小龙这类IM软件的方案，这种场景目前比较靠谱且简单的方式还是只有蓝牙或USB。

[https://localsend.org/](https://localsend.org/)

localsend是基于主动嗅探的设计来发现客户端，会遇到跨端找不到对方的情况。相比之下，另一款软件[sharik](https://github.com/marchellodev/sharik)会更简单好用，既能嗅探也能主动连接，可以在没有客户端的情况下直接用浏览器来接收文件。

最后，我卸载了localsend，用上了sharik。

## 5.QGIS-自由开源的桌面 GIS 软件
该项目采用 C++ 语言编写，GUI 部分使用的是 Qt 库。它提供了 GIS 数据可视化、编辑和分析的功能，支持多种 GIS 数据格式，适用于 Windows、Linux、macOS、BSD 和移动设备，大小约一个G。

![](res/gis.jpg)

然而下载下来发现自己不会用，没有一定GIS基础入门还是比较难的，也有可能是版本bug，按照网上教程windows版本的使用有一些问题，感兴趣的读者可以自行学习。我能想到的用途就是用来做一些自定义的地图，解决网上下载的那种通用地图所无法满足的场景。
[https://github.com/qgis/QGIS](https://github.com/qgis/QGIS)

国内有简单地图需求的可以使用 高德开发者平台或[地图慧](https://e.dituhui.com/login)。

## 6.Thunderbird Android 与 K-9 Mail的合并
Thunderbird 是 Mozilla 基金会开发的一款免费开源的跨平台电子邮件客户端，但目前为止 Thunderbird 仅可用于 PC 端。2022年夏，Thunderbird 开发人员在博客中证实，开源的 Android 电子邮件应用程序 K-9 Mail 将被改造成 Android 版 Thunderbird，填补 Thunderbird 在移动端的空白，也方便用户跨端同步数据。

以下是已公布的路线图：
1.使用 Thunderbird 帐户自动配置的帐户设置。
2.改进文件夹管理。
3.支持消息过滤器。
4.在桌面和移动 Thunderbird 之间同步
5.使 K-9 Mail 与 Thunderbird 的功能集和视觉外观保持一致

现在已经到了2023年，已经发布了几个Beta版本，路线图中的2和3已经基本实现，最有挑战性的莫非就是引入 Thunderbird 和 K-9 邮件帐户的同步支持了。这一项估计要到今年夏天才能实现。

在讲exchange的某期中已经提到K-9 Mail了，理所当然，K-9 Mail不会支持已经过时的exchange协议。

K-9 Mail最新版本下载地址：[https://github.com/k9mail/k-9/releases](https://github.com/k9mail/k-9/releases)

最后谈一个知识点：使用IMAP协议能实现近乎实时接收到新邮件推送，前提是该邮箱支持IMAP协议中的[IDLE](https://www.rfc-editor.org/rfc/rfc2177)命令。已知QQ邮箱和Gmail支持，163和sohu邮箱不支持。该推送机制不是系统级别推送，邮箱依然需要挂后台，只是省去了手动或定时刷新收件箱的操作。

ref:
[https://blog.thunderbird.net/2022/11/thunderbird-android-update-k-9-mail-6-400-adds-customizable-swipe-actions/](https://blog.thunderbird.net/2022/11/thunderbird-android-update-k-9-mail-6-400-adds-customizable-swipe-actions/)
[https://k9mail.app/](https://k9mail.app/)
# 读书与影视分享

## 1.日本2006年动画电影《红辣椒》

近未来，为了治疗现代人类越来越多、越来越严重的精神疾病，位于东京的精神医疗综合研究所开发出一种可以反映他人梦境的机器。通过微型DC的帮助，梦境在显示器上呈现出来，更方便找到一个人焦虑的症结。
某日，三台微型DC失窃，与之相关的研究人员的梦境接连被人侵入，随后受到严重伤害。美女医疗师千叶敦子另一个身份是梦境侦探“红辣椒”，她能够与患者同步体验梦境。为避免盗贼利用微型DC进一步作恶，她不得不潜入受害者的梦中寻找恐怖分子，一场充满奇幻和惊险的争斗旋即展开……

本片入围2006年威尼斯电影节主竞赛单元，荣获2007年葡萄牙奇幻电影节影评人选择奖、2006年蒙特利尔电影节大众选择奖。全片90分钟，豆瓣评分9.1分。

![](res/red.jpg)

> 对于梦境的描述让人叹为观止，梦境的碎片、跳跃、穿插无不让人印象深刻。


## 2.《晚清的世人与世相》
9世纪中叶到20世纪初，晚清中国因中西交冲而发生历史大变局，在回应西潮逼来的漫长过程里，传统文化养育出来的士人，作为七十年间回应西潮的主体，效西法图自强，深深卷入历史变迁的过程，一代一代地在古今中西之争中为民族寻路，因之而有前后相继的思想潮流和社会变革，与儒学相依的传统士人自身也发生了节节嬗蜕。

本书出版于2017年，汇积了作者对晚清士人及他们那个世界的思考、理解和解释，围绕着科举制度下的功名与富贵、世运盛衰中的学术变趋、晚清的清流与名士、十年新政与社会解体等主题，通盘解读近代化过程中的士人和社会，融深刻的洞察于历史叙述之中，很富于思想启发。

作者杨国强 ，1948年生于浙江诸暨，1953年迁居上海。1988年获华东师范大学历史学硕士，2003年被聘为上海社会科学院终身研究员 。现为华东师范大学思勉人文高等研究院教授。主要研究领域为中国近代史，尤其侧重于晚清知识分子与中国近现代社会变迁史的研究。

> 儒学经典中的很多章句都是说给人君听的，其用意大半在于警戒。读书人以“明道”为正路，学问和思想的起点即在这些章句之中。所以，沿着圣贤的话头讲下去本是非常自然的事。但谢济世以自己的祸难向天下士人说明，圣贤留下的道理当中也包藏着许多为时君所忮忌的东西，涉笔其间，便会成为一种危险。人人都怕靠近祸难。于是，在趋避危险的过程中，读书人与儒学精神的义理一面也离得越来越远了

# 图论

## 1.Living the dream

![](res/young.jpg)

ref:[https://www.instagram.com/mrs.frollein/](https://www.instagram.com/mrs.frollein/)
## 2.看飞机的人

![](res/plain.jpg)

> 安康富强机场位于秦巴山区，自2020年9月通航以来的两年半里，不间断地有来自附近区县村镇的乡民赶到机场看飞机。机场围栏外有一处高土坡，因视野开阔适宜观看，被踩得寸草不生。
>
> 中国有10亿人尚未坐过飞机，而站在富强机场外土坡上的人，很多都是第一次看到真正的飞机。

我是在30岁的时候，第一次坐飞机。

ref:微信公众号：真实故事计划（ID：zhenshigushi1），作者：吴向娟。
[https://www.huxiu.com/article/812333.html](https://www.huxiu.com/article/812333.html)
# 谈天说地

## 1.The End of the English Major
The crisis, when it came, arrived so quickly that its scale was hard to recognize at first. From 2012 to the start of the pandemic, the number of English majors on campus at Arizona State University fell from nine hundred and fifty-three to five hundred and seventy-eight. Records indicate that the number of graduated language and literature majors decreased by roughly half, as did the number of history majors. Women’s studies lost eighty per cent. “It’s hard for students like me, who are pursuing an English major, to find joy in what they’re doing,” Meg Macias, a junior, said one afternoon as the edges of the sky over the campus went soft. It was late autumn, and the sunsets came in like flame on thin paper on the way to dusk. “They always know there’s someone who wishes that they were doing something else.”

> 看完《纽约客》这篇巨长无比的大稿《英文系的终结》，终于相信美国高等教育系统的英文系这次应该差不多肯定是死了....
其实人文学科的危机喊了很久，英文系的生源减少、经费减少都快成祥林嫂式的抱怨了，我也不认为Nathan Heller能写出什么新鲜东西，甚至很怀疑炒这样的冷饭根本不需要写这么长的稿子。你完全可以用非常简单的数据证明英文系在美国快（已经）完蛋了，然后用雄辩的语言证明（其实是鸡同鸭讲）一下人文学科在这个时代的不朽价值。
Nathan Heller的稿子为什么这么长呢？因为他与其说是分析问题，还不如说是在一个前所未有的广阔光谱中以某种现象学的眼光来报道和描述英文系的境遇。稿子的前半程是大量的采访素材，从普通学生到毕业生，从大学教授再到大学行政人员，很少有人像Heller这样花这么长的时间、去往这么多地方、采这么多不同的声音。在这个意义上，《纽约客》的这篇稿子有很强的新闻价值。

> 文化战争的硝烟一直在烧，woke在带来学校与社会的深层分裂，中产阶级家长无法接受花那么多钱让自己孩子去大学里学习如何仇恨美国和全球资本主义；同时，以英文系为核心的激进性批判理论也走向了式微，文学研究和批评变得愈发琐碎和技术化，都是阳春白雪的专业大词。


ref:[https://www.newyorker.com/magazine/2023/03/06/the-end-of-the-english-major](https://www.newyorker.com/magazine/2023/03/06/the-end-of-the-english-major)
ref:[@洛之秋](https://weibo.com/u/1769741763)

## 2.双拼输入快速入门
> 换了类原生系统后，很多开源输入法没有了云联想的功能，全拼效率大大降低，加上部分输入法没有九宫格布局（fxtix-android，rime），双拼就成了一个更好的选择。

双拼不是对全拼的重新改造！只是一次对于键盘的重新定制，如是而已。

在全拼中，每个字都需要声母和韵母组成，但声母和韵母所需要输入的字母个数是不一定的，从一个到三个不等，按键时就需要进行多次输入才能组成一个声母或韵母。而双拼对其进行规范化，无论是声母还是韵母，都各自集合在一个按键上，即把声母中 zh、ch、sh 和 非单字母韵母（ong、iong、uang 等）进行重新编排，使每个声母或者韵母都对应一个按键。

![](res/sp.png)

ref:
[https://sspai.com/post/32809](https://sspai.com/post/32809)
[https://sspai.com/post/72622](https://sspai.com/post/72622)

## 3.巴别塔
巴别塔，也叫巴比伦塔，通天塔。

宗教传说中的“巴别塔”是《圣经·旧约·创世记》第11章故事中人们建造的塔。根据篇章记载，当时人类联合起来兴建希望能通往天堂的高塔；为了阻止人类的计划，上帝让人类说不同的语言，使人类相互之间不能沟通，计划因此失败，人类自此各散东西。此事件，为世上出现不同语言和种族提供解释。

不过，考古的发现和历史记载证实这并非神话，它确实存在过。巴别塔是新巴比伦王国的国王尼布甲尼撒二世主持修建或增建的一座高塔。

现在，“巴别塔”常用来隐喻理想化的工程或帮助翻越障碍的工具。比如有人把区块链、chatGPT（AI）比作巴别塔。

## 4.真的有让人说实话的药物吗
从古罗马时代，就有传说中可以使人吐露真话的药物。青少年小说《哈利波特》里的吐真剂，就是一种可以使人强制说真话的魔药。在相对现实的层面，现代间谍小说的里也有审讯药物的传说。

例如戊硫代巴比妥，就会减慢脊髓发送信息到大脑的速度，进而使说谎更加费力——但绝非不可能。

其实剥夺睡眠也可以带来同样的效果，所以经常用在刑讯逼供之中。只要您不是有病理性的说谎症(这种症状会使我们相信自己的谎言，无法区分想象与现实)，那么在思维变慢的时候，编造谎话就会变得极其困难。

尽管中情局，警察和纳粹审讯官在整个20年代，30年代和40年代做了很多尝试，但许多证据和科学报告表明，吐真药物具有其他副作用。其中最令人担忧的是，在半清醒的情况下，人们常常更容易被引导，说出审讯者想听的话。所以它在刑侦上并不是那么有用，而且现在已经是非法的。

历史上被人们寄予厚望的吐真剂有哪些呢？
1.硫喷妥钠(戊硫代巴比妥)
2.东莨菪碱(左旋-天仙子胺)
3.异戊巴比妥
4.乙醇
5.催产素

ref:[https://www.sciencealert.com/truth-serums-exist-but-they-probably-dont-work-the-way-you-think-they-do](https://www.sciencealert.com/truth-serums-exist-but-they-probably-dont-work-the-way-you-think-they-do)
# 一句话快讯

1.中国财政部数据显示，在31个省级行政区中，有11个存在养老金预算赤字，其中黑龙江省占比最大，占该省生产总值的负2.4%。中国社科院认为，中国养老金体系将在2035年耗尽资金。

2.拜登政府周四宣布对数十家中国实体实施出口限制，称这些实体的活动有悖于美国的国家安全和外交政策利益。
其中包括浪潮信息、华大基因、龙芯中科、第四范式等企业，以及国家并行计算机工程技术研究中心、青岛海洋科学与技术试点国家实验室、无锡先进技术研究院等研究机构。

3.3月2日晚，无锡市公安局发布消息称，该市当日举行涉疫个人数据销毁仪式，首批销毁数据10亿条，同时门铃码、疫查通等40多项“数字防疫”应用亦陆续下线。

4.我来（wolai）被钉钉收购。我来wolai是对Notion的本土化和“改造”，成立于2020年6月。创始人为前中文音乐星空、互联影库（Mtime时光网前身）创始人马锐拉（原名汪佳敏）。

5.3 月 7 日消息，统一推送工委会今日宣布，华为、小米、OPPO、vivo及其旗下子品牌全面支持[推必安](https://tuibian.mobileservice.cn/) 2.0 版本。据介绍，“推必安”是统一推送工委会推出的推送消息内容安全公共服务平台，可帮助开发者更好的规范传播内容。统一推送工委会近日在前期平台上开发升级了内容安全公共服务平台-“推必安”2.0 版本。

# 联系方式

啰里啰唆是一份针对互联网和生活爱好者的数字杂志，旨在发现和分享一切有趣的东西。话题不固定，每期大约十五分钟阅读量，暂定每周四发布。部分内容来自互联网采编，如果为有来源的转载，均会注明转载地址或保留水印。

这是一个关注人文和科技的newsletter。

使用方法建议或素材提供

频道：notonlyshare

邮箱：auokyob@outlook.com

github地址：[https://github.com/iminto/luoliluosuo-weekly](https://github.com/iminto/luoliluosuo-weekly)