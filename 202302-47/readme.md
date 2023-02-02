啰里啰唆周刊第47期：关关难过也要过

# 科技日常

## 1. ext4和XFS的预留空间
之前曾经聊过ext4和XFS和文件系统，ext4是许多Linux系统默认的文件系统，而自RHEL 7开始，XFS就成为了默认的文件系统,当然Centos 7也继承了RHEL 7的这一改变。在稳定性和容量上，XFS都是优于ext4的，至于性能，两者相差无几，没有明确、可靠的证据证明XFS性能低于ext4。因此，建议大家尝试下XFS文件系统。

文件系统通常都会有一个“预留空间”的概念，ext4和XFS也不例外。

当你买回一个1TB的新硬盘，放入一台装好了Linux的机器，然后Linux告诉你：这块磁盘的大小是977GB。怎么差了23GB，是Linux计算不准，还是硬盘制造厂偷工减料？

首先，差的并不是23GB，因为1TB并不是1000GB，而是1024GB，所以差的应该是47GB😂。这里以ext4文件系统为例，假设"df"的输出结果是这样的：
```bash
[root@somehost ~]# df -h
Filesystem             Size  Used  Avail  Use%  Mounted on
/dev/vdb1              991M  924M     0  100%  /mnt
```
显示总大小是991M，使用了924M，可怎么使用率就成了100%，用dd命令往磁盘里写点东西似乎也报错了
```bash
[user@somehost mnt]$ dd if=/dev/zero of=bigfile2
dd: writing to 'bigfile2': No space left on device
```
，同样的命令，切换到root用户再试试，又是成功的。
```bash
[root@somehost mnt]# dd if=/dev/zero of=root-file count=100
100+0 records in
100+0 records out
51200 bytes (51 kB, 50 KiB) copied, 0.000748385 s, 68.4 MB/s

[root@somehost mnt]# ls
bigfile  file3  lost+found  root-file
```
至于root用户还可以继续使用data block，原因是ext4文件系统为root保留了一些专用的磁盘空间，默认是5%，可以通过tune2fs工具的输出中的"Reserved block count"看。这个保留部分是可以调整的，一般调整为1%即可。

而XFS又有一点区别，与ext4不同，虽然XFS也预留了一部分空间，但这部分空间并不能被任何用户（包括root）所使用，而是留给XFS自己的，并且其大小要远小于ext4中保留空间在磁盘中的占比。

使用 xfs_io 命令可以查看到预留空间

```bash
[root@localhost home]# xfs_io -x -c "resblks" /
reserved blocks = 8192
available reserved blocks = 8192
```
一个size默认为4K，对于一个2T的分区，XFS也仅使用了32M的预留空间，远远小于ext4。

ref:
[https://www.redhat.com/sysadmin/disk-space](https://www.redhat.com/sysadmin/disk-space)

## 2. gocryptfs-基于文件的加密文件系统
这是一个基于文件的加密文件系统，默认模式类似于保险箱，在硬盘上保存的文件是加密的，用它可以 mount 出一个解密后的文件系统。另外它还支持 reverse 模式，也就是硬盘上保存的文件是明文，它可以 mount 出一个加密后的文件系统。

无论用哪种模式，用网盘备份加密后的文件就可以达到防止网盘扫描文件的效果。基于文件的意思是，加密／ reverse 是针对每个文件进行的。如果一个文件没有改变那它对应的加密／ reversed 文件也不会改变。非常适合网盘备份。与此形成对比的是VeraCrypt，其加密是针对整个盘/文件夹。

优先支持Linux，同时也支持Windows和安卓系统，以及第三方Python版本。

![](res/folders-side-by-side.gif)

[https://nuetzlich.net/gocryptfs/](https://nuetzlich.net/gocryptfs/)

## 3.Readwise Reader
Readwise  Reader=RSS+Newsletter+epub/pdf阅读器，最近大火的一个产品。

可以同时订阅RSS和Newsletter，还可以保存Twitter长串，YouTube视频好像还可以整理出字幕，还是EPUB阅读器！所有的文档都可以语音朗读、标注高亮。

readwise旗下有Readwise和Readwise Reader两个产品，Readwise是收费笔记软件，有两个月试用期，而Readwise Reader是单独的产品，目前在测试期，免费试用,也可以通过Readwise订购，为终生买断制。

![](res/reader.jpg)

[https://readwise.io/read](https://readwise.io/read)
[https://sspai.com/post/76574](https://sspai.com/post/76574)
[https://sspai.com/post/77349](https://sspai.com/post/77349)

## 4.开源灵感数据库
构建优秀产品，需要灵感，艺术的第一步都是模仿临摹,天才也难以逾越信息差的高墙，站在巨人的肩膀上会事半功倍，这个仓库的目标是收集灵感，追踪存活的灵感，复活陨落的灵感。

INS项目的灵感来自 阮一峰的网络日志 之 科技爱好者周刊，周刊每期都会带一些给读者带来灵感的项目，但没有给出方便查阅的项目导航列表，以及活跃项目持续追踪功能，于是本INS项目诞生了。

[https://github.com/zhaoolee/ins](https://github.com/zhaoolee/ins)

## 5.免费匿名电话号码——SafeUM

SafeUM官方网站：[https://safeum.com/](https://safeum.com/)
下载的时候可以在官网直接下载，但是iOS需要美区Apple ID，安卓需要在Google play下载，若你没有Google play，找一个apk文件也可以直接安装。下载需要注意防止假冒。

免费用户会强制看30秒左右的视频广告。注册并登陆后，进入设置，你就会看到一个免费的号码!接听电话免费，拨打需收费。

不建议作为高频常用号码使用，若有类似需求，可参考往期文章（第29期），购买海外实体卡。

## 6.SeeSharpSnake

用 C# 写一个小于 8KB 的贪吃蛇。这个项目的重点不是教你如何用 C# 写出一个贪吃蛇游戏，而是讲解怎么将编译后的 C# 贪吃蛇程序，从最初的 65MB 精简成 8KB 大小、可以独立运行的应用。

[https://github.com/MichalStrehovsky/SeeSharpSnake](https://github.com/MichalStrehovsky/SeeSharpSnake)
# 读书与影视分享

## 1.过昭关（2018年霍猛执导电影）- 小成本河南方言

《过昭关》是由霍猛自编自导，杨太义、李云虎、万众、聂栋才主演的乡村公路类电影，于2018年10月17日在第二届平遥国际电影节首映，2019年5月20日在中国内地公映。

暑假七岁的宁宁被送回乡下，由七十多岁的爷爷李福长（杨太义饰）照顾。李福长偶然间得到了一个老朋友的联系方式，得知老友身体中风，时日无多 。他决定骑摩托三轮车，带着孙子跨越千里看望老友。为抵达目的地见到自己思念的老友，李福长与孙子一路跋山涉水、马不停蹄，每天迎着朝阳出发，伴着夜幕入睡，一面在匆忙的旅途中感受社会百态与人情冷暖，一面又在磕绊的境遇中体验人生、思考生命。

该影片获得了第22届上海国际电影节电影频道传媒关注单元三项大奖，以及第32届中国电影金鸡奖四项提名。这是一部拍摄时长30天，成本仅40W的小成本电影，为了能够技术达标，在院线上映，声音部分约占了电影总投资的40%。小成本制作加上河南方言演出，霍猛决定找非专业演员的农民来参演。

**累计票房不到50W，故事也俗套，没有任何明星，但是仍值得一看。**

![](res/guo.jpg)

> 《过昭关》是一部朴素、悠然、气定神闲的公路电影，它以祖孙二人的一段生命之旅、向观众讲述了这个时代稀缺的善意。主题与手法的朴实无华，给人们带来了意外的感动与思考。影片的通达、自然、以及毫不矫揉造作，在电影中显得尤为重要

> 全片最大的感受就是镜头十分优美，每一帧画面都可以当壁纸，完美展现了乡村公路的自然风光和乡土人情！一路上宁宁和爷爷学到了很多，也成长了很多，过昭关的故事十分吸引人，第一次了解到这部戏剧的历史。第一次听还觉得和电影不搭，最后片尾大雪纷飞配上老爷爷独自唱这出戏十分凄凉，物是人非，让人觉得韵味悠长，耐人寻味。主题体现了人生的许多道理，关关难过也要过！



## 2.《The Thing in the Snow》

The Economist推荐的2022年度书籍之一，反乌托邦作品。

Sean Adams has dialed down the dystopian quotient from his first satirical novel, The Heap, but that element is still very much present in The Thing in the Snow. 

Workers try to hold onto their sanity as they maintain a desolate, snow-covered research station in Adams’s dryly funny absurdist latest (after The Heap). Each week, a remote administrator named Kay assigns a meaningless task to Hart, the on-site manager at the obsolete Northern Institute, for Hart to accomplish with his subordinates Gibbs and Cline, their employer having deemed it more cost-effective to keep the place running than to close it down. The crew spends their time testing the noisiness of doors and the stability of chairs, and doing their best to avoid Gilroy, the sole remaining researcher (according to Hart, Gilroy is the type who, when encountered, elicits ‘distaste that is not just warranted, it is the correct evolutionary response’). One day, the men spot something in the snow. The distraction annoys Hart, who views the development as a threat to his already tenuous leadership. After Gibbs reports the object to Kay, Kay replies, ‘if immobile, not of concern.’ Consequently, the crew members become irrationally convinced that the barely perceptible object is moving. The workplace gags are effective, and as the workers turn on one another, things really take off. The strange blend of satire, mystery, and psychological thrills make for a winning combination.

[https://www.bookpage.com/reviews/the-thing-in-the-snow/](https://www.bookpage.com/reviews/the-thing-in-the-snow/)

## 3.《Never Give An Inch》

美前国务卿 迈克·蓬佩奥（Mike Pompeo）于2023年1月出版的回忆录。内容不做过多介绍，感兴趣的读者可以自行查阅。
# 图论

## 1.The Social Pressure Season Is Officially Open

![](res/chick.jpg)

[https://www.instagram.com/depression_chicken/](https://www.instagram.com/depression_chicken/)
## 2.这是什么？
![](res/head.jpg)

你可能想知道那是什么鬼东西。可能是某种变异的人形头骨？
其实完全正常。你现在看到的是一个人类幼儿的头骨。
原来，幼儿的恒牙在他们的眼睛下面。随后，当乳牙脱落时，它们会迅速就位。


# 谈天说地

## 1.从《上古卷轴》、《荒野之息》再到《原神》：沉浸模拟游戏研究笔记
本文旨在面向游戏策划相关岗位或者对游戏设计感兴趣的读者，分享一下个人对于【沉浸模拟】游戏的相关研究笔记，并交流一些想法。可能会有大量专业名词/黑话，而且行文会比较生硬，还请多多见谅。
本文仅作研究/教育之用。所有版权物归属各个版权方。所有转载需注明出处。

沉浸模拟游戏的共同点：

横向多解的难题：每一个玩家需要解决的问题都有多个解法。
规则系统：游戏中有数个规则系统（游戏机制）如【温度】【重力】【潜行】，玩家可以自由利用规则解决难题。
高可互动的游戏世界：如《上古卷轴》系列中世界中放置的小刀、盘子等，都是可以拿起来互动的物品。

这样的游戏整体设计完美地满足了【易上手难精通】的设计目标，且同时提供了【沉浸感】+【自由度】，喜欢RPG体验的休闲玩家和喜欢挑战自己的硬核玩家都可以找的自己的乐趣。

[https://www.gcores.com/articles/160299](https://www.gcores.com/articles/160299)

## 2.中国到底哪里的凉粉最好吃
凉粉，是中国人对抗炎夏的秘密武器。

无论天多热，当那份浸润着不同料汁的凉粉，穿舌过喉在身体内长驱直入时，整个夏天就变得清爽且熨贴。它们，是夏日美食的主旋律，是必不可少的一碗清凉。

![](res/liangfen.jpg)

**咱吃的凉粉不是同一种吧？** 当天南地北的小伙伴们坐在一起郑重讨论凉粉时，这个问题是不可避免的。

我们常见的凉粉，白白嫩嫩，多以淀粉（豌豆粉、大米粉、土豆粉、绿豆粉、荞麦粉）为原料，与水混合、加热搅拌，不一会儿锅里变得浓稠，盛出冷却后羊脂玉般莹润。看一眼，就让人觉得清凉。

**陕西臭凉粉**

秦岭腹地，陕南地区有一种与大山同色款的凉粉，当地叫“神仙凉粉”（有地方也叫神仙豆腐），几年前在西安的美食节上赚足了眼球。

![](res/chouliangfen.jpg)

每年春天，当地人都会去山上找“臭老汉”。臭老汉不是做凉粉的人，而是制作凉粉的原料，学名叫六道木（有的地方也叫臭黄荆）。嫩叶采下洗净后，放入桶中，加入烧开的山泉水，反复搅拌成糊状，倒入滤布、压出浆汁，再加入柏树草木灰搅拌均匀，放在阴凉处冷却凝固两个小时，神仙凉粉就做成了。

这种凉粉的做法，实际上是明代时由湖广移民带来的。如今，这种凉粉在湖广地区已经很少见了，倒是重庆巫山一带还见得到，当地人还为它还取了个别致的名字：翡翠凉粉。据说，在改名前，它还有一个“臭盐菜凉粉”的乳名，莫名地叫人心疼。

**两广仙草凉粉**
两广地区之所以“抛弃”臭老汉，是因为他们找到了另一种名字更优雅的原料——仙草。仙草也叫凉粉草，富含凝胶性多糖类物质，煮过之后，把它的精华都搓出来，倒入锅中加热搅拌，再加入粘米粉，晾凉凝结后，便是bulingbuling的“青凉粉”（白凉粉）。如果用干凉粉草做原料，得到的就是一份细嫩爽滑的“黑凉粉”。

**丽江鸡豆凉粉**
无独有偶，云南丽江也有“黑凉粉”。只不过这种凉粉的原料，是当地特产的“鸡豆”。这种豆因大小与鸡眼睛相仿而得名，制成的黑凉粉也叫黑豆腐，与两广地区的黑凉粉完全是两种模样。鸡豆凉粉虽其貌不扬，吃起来却细腻滑爽，由于极适口，常被当地人当下酒菜来吃。

**宁波薜荔凉粉、云南冰粉**
浙江宁波、绍兴两地的凉粉，以及江西的白凉粉，所用原料是薜荔籽。记忆力好的童鞋，或许还背得出《从百草园到三味书屋》中的那句“何首乌藤和木莲藤缠络着，木莲有莲房一般的果实，何首乌有臃肿的根。”鲁迅先生所写的木莲，便是薜荔。

用薜荔籽做凉粉，与西南地区用假酸浆做 **冰粉**的手法相似。假酸浆原产秘鲁，明代时一进入中国，就被做成凉粉摆上了餐桌。

薜荔不是假酸浆，两者不是同一种植物，口味也不同，但两者的相似之处是制作手法几乎一模一样。

假酸浆的籽只有芝麻大小，却富含果胶，收集起来用纱布包好，放在清水中搓啊搓，果胶就释放到了水中，不一会儿清水就变成了浅黄色，再加点石灰水，就凝固好了。现在许多餐饮店的冰粉，都是用冰粉粉末冲兑成的，无色透明，口感大不如手工搓制的。

因为可以做凉粉，假酸浆籽就赢得了“凉粉籽”的美名。在云南地区，假酸浆还被称为“酸木瓜”，用假酸浆籽制作的凉粉，则被称为“木瓜水”、“木瓜粉”，其实，它和木瓜半毛钱关系没有。

冰粉流行于西南地区，其中于云南冰粉最出名，配料最丰富，米虾仁、玫瑰糖、芝麻、酸梅汁等一股脑加进去，在解暑这件事上，充满了“丰盛的仪式感”。

![](res/mugua.jpg)

宁波人把“薜荔水”叫做凉粉，云南人把“假酸浆水”叫做木瓜粉，云南的普通凉粉一般是豌豆粉或荞麦粉制作，当然由于云南地区复杂，制作手法和材料比较多。

**青岛石花菜凉粉**

同样晶莹可人的，还有山东青岛的石花菜凉粉。它的原料，是长在沿海礁石上的石花菜，也叫牛毛菜，浸泡后煮至粘稠，过滤冷却便成，看起来像果冻一样，吃起来爽利嫩脆，跟海岸边的夏天般配极了。

除上述地区外，大多数地方做凉粉的原料，其实都是淀粉。但单就是淀粉，在千百年的时间里，也足以花样百出、“千人千面”。

**甘肃、巧家荞麦粉**

**甘肃陇东一带**，将荞麦仁用水泡软后，装进干净的布袋中，放在水盆里搓出荞麦仁里的淀粉，再倒入锅中加热搅拌，烧开后盛出晾凉，就是典型的陇东凉粉。而在距陇东1600千米的**云南东北部，昭通市巧家县**也用荞麦做凉粉，不同的是巧家人会先将荞麦磨成颗粒，放入水中浸泡几个小时，再搓出其中淀粉，做成云南著名的巧家凉粉。

同样以荞麦为原料，制作凉粉的，还有贵州毕节织金县。织金人做凉粉，用的是苦荞，做法与巧家县大同小异，当地人称之为“荞凉粉”，也是毕节一大著名小吃。山西吕梁一带，也有用荞面制作凉粉的，当地叫做“碗秃”，筋软耐嚼、香醇可口，有生意头脑的人将此物引入晋中，成为平遥古城里地方特色明显的小吃。

**山西土豆凉粉**

**晋北**人则选择了土豆。大同浑源县，以土豆淀粉制成“浑源凉粉”，“拿在手上滑溜溜，吃在嘴里凉丝丝”，风味独特，堪称北岳一绝，已被列入山西省非物质文化遗产名录。浑源隔壁的应县，也用土豆淀粉做凉粉，但应县的凉粉含水量较大，且在吃之前一直浸在水中，故而当地人不说吃凉粉，而说“喝凉粉”。

**川北米凉粉**

**川北地区**，则将大米与石灰水浸泡，再磨成浆，小火熬到似滴非滴时盛出晾凉，就是米凉粉，也叫川北凉粉，只是这种凉粉吃起来不够筋道，对吃惯了其他淀粉类凉粉的人来说，没有什么嚼劲儿。

青海、陕西关中地区、重庆潼南区、安徽阜阳地区、河南确山县、贵州遵义等地，一般都选择绿豆粉或豌豆粉来制作凉粉。口感如何，就要在各地不同的料汁与烹饪方法中见分晓了。

各地最常见的吃凉粉方法，是凉拌和煮。但是河南炒凉粉是其中奇葩之一。

**河南炒凉粉**

凉拌的凉粉吃够了，于是**“炒凉粉”**横空出世。这种奇特的吃法，到底源于何时何地，没有人说得清。从中原地区的河南，到西北地区和西南地区，到处都有炒凉粉的影子。

河南开封炒凉粉时，会将做好的凉粉切成指头蛋大小的方块，而甘肃武威则切成一寸见方的块，四川阆中则是切成薄片，江苏连云港则会切成面条状，或漏成娃娃鱼状……各地炒凉粉时，都会有自己独特的切法，但殊途同归，这些切好的凉粉，最终都会在一锅炝了葱、姜、蒜的热油里，完成自己的“蜕变”。

至于口味，见仁见智了。河南炒凉粉，可以说是河南四大黑暗料理之榜眼（毛蛋，炒凉粉，爬蚱，胡辣汤）。。。其实炒凉粉的关键在于材料，而不是炒制手法。

ref:[https://baike.baidu.com/tashuo/browse/content?id=1fc949137783861d62aa39a5](https://baike.baidu.com/tashuo/browse/content?id=1fc949137783861d62aa39a5)


## 3.刘锡鸿：仿造西洋火车无利多害折
1880年刘铭传、李鸿章上书清国朝廷要修铁路。李鸿章还专门写了《妥筹铁路事宜折》提出修建铁路有九大益处。

但出使过英、德、奥、荷，亲自坐过铁路的清国外交官刘锡鸿却反对修建铁路，并针锋相对写出了《仿造西洋火车无利多害折》提出修建铁路有“不可行者八，无利者八，有害者九”表示大清国万万不可修建铁路。

结果朝廷听取了刘锡鸿们的意见，帝师翁同龢甚至认为“看刘云升(锡鸿)奏铁路不可修状，言言中肯”。

你可能觉得刘锡鸿是个愚不可及的笨蛋，他亲眼看过铁路、坐过铁路，知道“火车之利于遄行，速者一昼夜三千里，缓亦一千数百里”怎么还竭力反对呢？

恰恰相反，刘锡鸿并不是个傻瓜，他提出的反对意见有还颇有一些真知灼见，甚至可以说预言了清政府的倒台。

《仿造西洋火车无利多害折》 

奏为中国情形，种种不同西洋，仿造火车势不可行，无利 而多害，恭折缕陈所见仰祈圣鉴事。窃闻近有建议仿造火车铁 路者，此等创举，朝廷自必深思博访，确见妥善然后施行，决无 徒听数人私言，遽兴大工之理。然臣顾亟亟言之者，无事生事， 人心惶惑．物议沸腾，甚非国家之福。臣尝奉使西洋，讲求其事，既有所见，不敢不即陈明，以期早日罢论，息此纷纭也。

夫火车之利于遴行，速者一昼夜三于里，缓亦一千数百 里；而且一机器居前，能缀十数车于后，每车上下兼坐，可容百 数十入； 行不颠簸， 亦不晕眩；虽崇山峻岭，巨壑深潭，穴以通 车，则悉成平地，而无攀跻过涉之苦。此实古今之奇观，绝世之 巧术，臣虽愚拙，亦乐其便，冀以施诸中华。是以驻英、驻德使 事余暇，即遍览其纵横之道，履其制造之局，与其巨商、老匠悉 心推求，而又博考诸各国豪酋及波斯、日本、土尔奇等国非西 洋而效为西洋火车者，朝夕以思，如此者两年，乃叹火车实西 洋利器，而断非中国所能仿行也。臣窃计势之不可行者八，无 利者八，有害者九，敢请为皇太后皇上详细言之 

[https://zh.wikisource.org/wiki/仿造西洋火车无利多害折](https://zh.wikisource.org/wiki/仿造西洋火车无利多害折)
[https://baijiahao.baidu.com/s?id=1650169429625064545](https://baijiahao.baidu.com/s?id=1650169429625064545)

## 4.The happiest, least stressful, most meaningful jobs in America
Agriculture, logging and forestry have the highest levels of self-reported happiness — and lowest levels of self-reported stress — of any major industry category, according to our analysis of more than 13,000 time journals from the Bureau of Labor Statistics' American Time Use Survey. (Additional reporting sharpened our focus on lumberjacks and foresters, but almost everyone who works on farms or in forests stands out.)

The time-use survey typically asks people to record what they were doing at any given time during the day. But in four recent surveys, between 2010 and 2021, they also asked a subset of those people — more than 13,000 of them — how meaningful those activities were, or how happy, sad, stressed, pained and tired they felt on a six-point scale.... [H]appiness and meaning aren't always correlated. Heath-care and social workers rate themselves as doing the most meaningful work of anybody (apart from the laudable lumberjacks), but they rank lower on the happiness scale. They also rank high on stress.

The most stressful sectors are the industry including finance and insurance, followed by education and the broad grouping of professional and technical industries, a sector that includes the single most stressful occupation: lawyers. Together, they paint a simple picture: A white collar appears to come with significantly more stress than a blue one. 

[https://www.washingtonpost.com/business/2023/01/06/happiest-jobs-on-earth/](https://www.washingtonpost.com/business/2023/01/06/happiest-jobs-on-earth/)

## 5.诡异的虚无僧
ACG作品中的日本僧人，为什么经常在脑袋上戴个“箩筐”？他们身披长袍袈裟，脚上穿着普通的草鞋，他们的头上戴着一个竹编的像箩筐一样的东西，不将自己的面目示人。
![](res/seng.jpg)
日本曾有着一种不剃度不住寺院，却吹着尺八云游列国的名为“虚无僧”的僧人存在。

说起虚无僧的起源，就要追朔到日本的镰仓时代与室町时代之间的南北朝战争，那时的日本同时有南北两个朝廷，两个朝廷相互对抗常年战争，最终以南朝廷的灭亡为战争画上了句号。而在南朝廷灭亡以后，活下来的一名名为楠木正胜的武将预谋再次起兵反抗北朝廷，便入了普化宗为僧冠名“虚无”，并在之后头戴“天盖”，口吹尺八，身带佩刀，周游列国。由此，楠木正胜的形象便成为了普化宗僧人在一般人心中的形象，普化宗的僧人也开始被普遍的称之为“虚无僧”。

一般来说，所谓的僧人皆是皈依佛门之人，但对于普化宗的“虚无僧”来说却并非如此，因为“虚无僧”自身的性质就决定了其不会只是单纯的僧人。

在明治4年（1871年），普化宗遭到了废宗。自此以后，原本数量众多的“虚无僧”数量骤减。原本只有虚无僧才能吹奏的尺八也成了一般平民可以学习的技艺。
[https://www.douban.com/note/813254204/](https://www.douban.com/note/813254204/)
[https://www.gcores.com/articles/161048](https://www.gcores.com/articles/161048)

## 6.1930s世界往事：发展与安全
安全诉求的提升与逆全球化也曾同时出现于1930年代。彼时政府开支多有扩张，政府、国有型企业在经济中的重要性上升；同时资源的重要性正在系统性提升，“神奇的橡胶”成为最重要的储备。当下投资问题的答案，或许在90年前已经写好，我们只需要突破对过去10年历史的经验主义依赖。

摘要
1.突破短期历史经验的局限，寻找超额收益来源。

2.英国的1930s：从“十年规则”到重整军备。

3.德国的1930s：经济复苏与“四年计划”。

4.美国的1939—1941：战略资源储备。

5.不一样的“投资思路”启发：发展是安全的基础，安全为发展提供保障是1930s年代的历史注脚。

ref:[https://mp.weixin.qq.com/s/-IOvDA2WXRJK557n7Hf_rw](https://mp.weixin.qq.com/s/-IOvDA2WXRJK557n7Hf_rw)

## 7.比尔·盖茨成全美最大私人农田“地主”
昔日科技巨擘比尔·盖茨有了新身份——美国最大私有农田 “地主”。根据2022年版《土地报告100》（The Land Report 100）的数据，比尔·盖茨已经在美国拥有超27万英亩农田，这相当于1090平方千米多土地，接近北京通州区的面积。

此前，比尔·盖茨1月中旬参加了社交新闻网站Reddit的“问我任何问题”（Ask Me Anything）活动，在被问到拥有大量农田的原因时，回应称：“我拥有的农田不到美国的1/4000。我的投资是为了提高它们的生产力，创造更多的就业机会。这其中没有什么宏伟的商业计划。事实上，所有这些都是专业投资团队做出的决定。”

据农业创投媒体AgFunder的报道，在过去十多年里，比尔·盖茨持续透过旗下投资公司Cascade Investment收购全美各地的农地，并在比美国19个州拥有农业土地。

ref:[https://finance.sina.com.cn/tech/roll/2023-01-29/doc-imycvpiv0408997.shtml](https://finance.sina.com.cn/tech/roll/2023-01-29/doc-imycvpiv0408997.shtml)
# 一句话快讯

1.据初步统计，2023年春节档（除夕至正月初六，1月21日至1月27日）电影票房为67.58亿元，同比增长11.89%；观影人次为1.29亿，同比增长13.16%；国产影片票房占比为99.22%。春节档上映的6部影片累计票房分别为《满江红》26.06亿元，《流浪地球2》21.64亿元，《熊出没·伴我“熊芯”》7.48亿元，《无名》4.93亿元，《深海》3.59亿元，《交换人生》2.9亿元。截至2023年1月27日，全年总票房为79.15亿元，同比增长209.88%。

2.香港电话卡实名登记制度将于2月23日起全面实施，届时未完成实名登记的电话储值卡(太空卡)将不能使用。

3.著名翻译家杨苡先生于2023年1月27日晚20:30驾鹤西去，享年104岁。因翻译《呼啸山庄》闻名于世。

4.珠海部分行首套房贷利率低至3.7%，为全国最低，1月30日起执行。

5.Spotify 月活用户增长超出预期，预计下季度将达 5 亿里程碑。

6.全国GDP排名前十城市均已公布2022年经济成绩单。武汉2022年GDP实现了对杭州的超越。根据官方公布数据显示，2022年全国城市GDP十强为：上海、北京、深圳、重庆、广州、苏州、成都、武汉、杭州和南京。按照各地统计局发布的数据，2022年，中国城市前五名排位为：上海（44652.8亿元）、北京（41610.9亿元）、深圳（32387.68亿元）、重庆（29129.03亿元）、广州（28839亿元）。

7.美国拜登政府星期一（1月30日）宣布，实施了将近三年的冠病紧急状态将在5月11日后正式结束。

# 联系方式

啰里啰唆是一份针对互联网和生活爱好者的数字杂志，旨在发现和分享一切有趣的东西。话题不固定，每期大约十五分钟阅读量，暂定每周四发布。部分内容来自互联网采编，如果为有来源的转载，均会注明转载地址或保留水印。

这是一个关注人文和科技的newsletter。

使用方法建议或素材提供

tg频道：notonlyshare

邮箱：auokyob@outlook.com

github地址：[https://github.com/iminto/luoliluosuo-weekly](https://github.com/iminto/luoliluosuo-weekly)