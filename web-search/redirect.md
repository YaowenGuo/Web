[Ranking factors session recap from SMX Advanced 2018](https://searchengineland.com/ranking-factors-session-recap-from-smx-advanced-2018-300383)

文章整理了SMX Advanced会议（搜索引擎营销大会）上三位发言者关于SEO排名影响因素的发言笔记，
Marcus Tober(Searchmetrics)认为谷歌在将最佳用户意图映射到每个搜索查询方面取得了巨大进展，并且在每种查询类型中都不同。
Mordy Oberstein(Rank Ranger)认为。SEO的未来在于意向分析，应当去了解谷歌是如何在你的内容和你的关键词中看到潜在的意图的
Jeff Preston(Disney)认为，SEO领域中我们非常容易被海量数据误导，因此参考的案例研究必须来自信任的对象，并尽量自己亲自做测试得到数据；此外他分享了一些自己做的SEO影响因素的测试结果


[2. Mordy Oberstein：Beyond the Factors - A Machine Learning Love Story ](https://www.slideshare.net/SearchMarketingExpo/beyond-the-niche-beyond-the-factors-a-machine-learning-love-story-by-mordy-oberstein)

- 调查表明2015年到2016年相同关键词查询结果变化非常大
- 测试发现搜索结果页面40%是信息性页面（informational），电商网站可以考虑揣摩用户意图，增加信息性页面以获取流量
- 应当揣摩Google如何看待你目标内容和关键词相关的用户搜索意图，据此确定优化重点


[3. Jeff Preston：What's Important, What's Not
](https://www.slideshare.net/SearchMarketingExpo/seo-ranking-factors-in-2018-whats-important-whats-not-by-jeffrey-preston)


NO RANKINGS IMPACT
- 大量站点从HTTP移动到HTTPS——未看到实际影响
RANKINGS IMPACT
- 删除八万各低质量URL——立刻出现大规模流量激增
						——由于删除重要的301重定向，一段时间后流量暴跌
- AMP(accelerated mobile pages)——对美国网站影响很小；对其他国家如英国影响较大
- 更换domain——两个案例结果不同，一个恢复时间26weeks+，一个4weeks
- canonical loop

[Google begins sending goodbye old ADWords UI notices](https://searchengineland.com/google-begins-sending-goodbye-old-adwords-ui-notices-300660)

三月份Google推出新的 ADWord（关键词竞价广告，CPC计费）界面，宣布在年底前完成改版；本周有广告商先后收到通知，他们的账户将在七月开始切换到新界面。接下来Google将对所有广告主进行滚动时轮流改版，预测新界面将在十月份完成全部切换。

[5 things to check if your traffic suddenly drops
](https://searchengineland.com/5-things-to-check-if-your-traffic-suddenly-drops-300025)

1. Significant changes to your site
2. Manual search engine penalty
3. Google algorithm update
4. Valuable backlinks lost
5. Competitors and SERPs changes



[2018 Search Marketing Expo](https://searchengineland.com/ranking-factors-session-recap-from-smx-advanced-2018-300383)

文章里面提到的经过亲自验证的几个SEO的case，一一对比了Coupon目前的情况，结论如下：

1和2很简单，大家都能理解，我们现在也不存在这个问题；
3这个概念很多不同学不懂，可以好好看看，是个SEO雷区，虽然我们任何项目还没有经历过，但是可以了解一下，小心绕过；
4和5对于Coupon项目有影响，这些case会对我们接下来的项目操作有引导作用，重点看；

Http to Https: 升级网站证书对于排名没有任何影响，Google官方的声明是这么说的，其他站长的一些案例测试也证明了，在http升级到https前后流量基本无差别；Coupon目前已经升级到https，后续的其他项目也都会用https，目的是为了访问安全性；

Change Domain：关于换域名，过去我们几个项目都尝试过，从我们自己经验和文章中的案列来看，没有正面的影响，换域名后流程需要几周到3个月甚至半年不等的流量恢复期，有意思的是确实换了域名之后在流量回复的过程中会出现一个spark，但是这个spark很短暂，也就几天时间；另外换域名对于外链的权重流失的影响也是比较严重的；后续我们的项目不会考虑这种操作方式；

Canonical Loop：有的同学对于canonical不太理解，简单来说canonical就是一种在代码中呈现的标签，它的主要作用是用来解决由于网址形式不同内容相同而造成的内容重复问题；举个例子，以coupon为例，我们有https://www.couponbirds.com/coupon-specialist这个页面，里面每一个同学profile也会生成一个新的url：https://www.couponbirds.com/coupon-specialist?name=lucy，那这两个页面实际在内容上是重复的，google收录两个重复的页面对于排名并不友好，当然它会自己挑选哪个合适来作为优先排名，为了避免权重的流失，同时让google更好的收录，就会用到canonical这个标签，在https://www.couponbirds.com/coupon-specialist?name=lucy网页代码里添加<link rel=”canonical” href=“https://www.couponbirds.com/coupon-specialist” />，意思就是告诉 Google不要给https://www.couponbirds.com/coupon-specialist?name=lucy页面rank，这两个页面内容重复，请以https://www.couponbirds.com/coupon-specialist为准；这个标签我们实际项目中很少使用，对于这种因为参数比如排序或展示引起的重复页面，我们选择直接在robots里面屏蔽收录，就让Google捕捉一个页面；这篇文章专门提到了一点Canonical Loop是什么意思呢，比如网页www.abc.com和abc.com是重复页面，如果你设置了www.abc.com canonicalize to abc.com(以abc.com收录为准)，但是又把abc.com 301 指向了www.abc.com，这样就形成了一个loop（循环），这个循环会有什么危害？你的网站基本就垮了，Google就对任意一个网页也不排名了，自然搜索流量暴跌，SEO基本废掉；同时案列提到Google现在有注意，去fix这种问题，但是貌似没有任何效果，如果一个网站这样做了，Canonical Loop=SEO Death。我们现在项目没有用到这种操作手段，但是值得引起注意，不要踩到雷区。

AMP：网络专业人士多年来一直重视创建“移动互联网站”。诸如响应式网页设计的实践旨在帮助创建适用于所有设备的网站，并将重点放在网站性能和快速下载时间上，使所有用户，移动设备或其他用户都受益。移动友好网站的另一种方法被称为AMP Web开发，代表加速移动页面。AMP最近两年很火，Google也在主推，Coupon项目目前是偏响应式web开发；根据文章中案例，AMP对于US mobile traffic的影响很低，基本不变，其他国家，比如英国，巴西，出现了增长的情况；找了一些其他关于AMP对SEO影响的文章，普遍的结论是有帮助，但是对流量有多大的帮助意见不一，可能也因站而异；关于AMP web开发，既然这是一个趋势，Google在主推，对于SEO有一定价值，Coupon项目可以去调研尝试。

删除低质量页面：这个case很有指导意义；大数据在coupon的流量变化上印证的十分明显，目前coupon处于一个瓶颈期，数据量和质量出现了不平衡，量级越来越大，低质量的比例越来越高，Google index的数据在最近几个月的停滞侧面证实了文章中的观点；所以18年一月份的时候我们停止了user的新增，担心对于流量的损失情况并没有发生；website的新增6月份刚刚控制住，也停止了自动化；但是站内目前已经有100万的页面了，低质量的比例超50%，对于这部分的处理，之前的方案是拿掉所有的内链，sitemap正常保留，从文章中的case来看，我们在sitemap包括ＧＷＴ中，理应对这些低质量的页面进行移除而不是保留；当然文案列中有特别提到，如果有的一些页面做了301，比如A跳转到B，即使已经两年之久，如果把A拿掉，B的流量还是会受影响（文中的case是出现大量的301情况，然后移除，造成的流量下跌，如果个别几个问题不会太大），但是这个反应SEO值得注意的一个事项，这个点要关注，后面项目可能要注意操作。
