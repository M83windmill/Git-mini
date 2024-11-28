Rayban 评论

# 概述

需求：从数据分析中发现更详细的产品形态&功能指向，包括：穿戴体验（外观、重量、舒适度）、音频（听、录）、影像录制（清晰度、使用体验）、AI（场景、效果）、其他使用场景续航、价格等维度。

本篇报告包括：

1. 数据概述：数据集的构成，主要结论
2. 总体数据的维度，以及维度详情
3. 数据处理方法与理论 

# 数据总体分析

### 数据集简介

本次数据采集了Meta官方商店，Best Buy，Amazon 三个来源，共计1550条评论。其中Best Buy平台有是否向其他用户推荐的特殊指标，推荐率为93.3%

各个来源的评论数据概览如下：

|               | 评论总数 | 平均分 | 满意率 | 中立情感 | 不满意率 | 推荐率 |
| ------------- | -------- | ------ | ------ | -------- | -------- | ------ |
| meta_official | 126      | 3.897  | 0.333  | 0.317    | 0.349    | N/A    |
| Amazon        | 394      | 3.685  | 0.378  | 0.284    | 0.338    | N/A    |
| Best Buy      | 1030     | 4.625  | 0.545  | 0.350    | 0.105    | 0.933  |
| 总计          | 1550     | 4.327  | 0.485  | 0.331    | 0.184    | N/A    |

注解：

1. 分类定义方式：

"满意率": "如 很支持此产品，相当值得推荐 这种强烈的语气",

"不推荐": "如 不推荐，对此产品不满意",

"中立情感": "没有明确推荐情况，无明确的支持和反对"

1. 推荐率说明：Best Buy平台的特殊指标，即 是否向其他用户推荐这款产品
2. 关于平均分：三个数据来源均有对产品进行1-5分的打分，即 5 out of 5 stars

# 数据处理方法

### 方法概述

将不同数据结果汇总清洗，构建评论集全特征空间

从评论数据集中批量抽取评论，将评论不断组合，得到数据的评价指标集合；

将评价指标集合经过累加，得到一个大型的评价指标分类树；

然后使用GPT将全量数据按照此分类树进行分类评价

### 采样与组合：

通过从评论数据中采样和组合提取共同评价指标，是一个**自底向上构建特征空间**的过程，具有良好的代表性。能提取出具备共性且可推广的评价指标，有助于减少噪声数据对模型的影响。

### 评价指标分类树的构建：

评价指标分类树通过层层细分的结构来组织各类评价指标，符合**层次分析法**的基本思路**。**构建评价分类树是一种聚类方法，使得评论内容能够聚集到对应的评价类别中，减少数据复杂度，提高模型对新数据的泛化能力。

### GPT对全量数据分类：

调用GPT进行

GPT的语义分析和自动标注能力增强了分类效果，它可以从分类树提供的上下文信息出发，对不同评价指标的含义作出细致区分，避免了普通分类算法对复杂文本理解的局限性，符合机器学习的泛化性原则。

# 总体分析结果

### 评价维度方面

在本表中，将用户评论提及的共性拆解为以下方面，按照 评论总提及数量 降序 排列

| 维度                     | 评论总提及数 | 好评占比 | 实例                                                         | 解释                                       |
| ------------------------ | ------------ | -------- | ------------------------------------------------------------ | ------------------------------------------ |
| 播放音质                 | 561          | 91.62%   | Love these glasses. Only complaint is the battery life but they charge quickly in the case and the case lasts me about a week. I really like these glasses. Photos and videos are great and the sound is awsome. Use them mostly for calls and watching some videos. | 在播放音乐和媒体时的音质                   |
| 相机性能                 | 491          | 82.50%   | Brought these glasses for my husband who loves all thing tech, and they have lived up to there hype! The picture and video quality is top tier. Glasses are lightweight and stylish. | 不同环境下的性能                           |
| 拍照便利性               | 468          | 88.89%   | Great glasses for on the go recording and pictures. Battery life is better than expected and sound quality is too. | 能够快速拍照和视频的功能                   |
| 外观设计                 | 431          | 94.43%   | I will recommend for everyone. It’s very classy and smart    | 时尚外观                                   |
| 续航时长                 | 251          | 40.63%   | Solid design, great battery life<br>Very exciting!           | 电池续航评价                               |
| AI助手的便捷性和智能响应 | 240          | 88.75%   | This can take beautiful photos and movies as I see with just simple action.<br><br>Nice camera, nice speaker, nice microphone, cool AI with stylish frames | 响应速度，与其他设备集成                   |
| 通话音质                 | 208          | 82.21%   | pictures are clear, video is clear, music sounds great, people can hear me talk clearly when using it for the phone.. absolutely zero regrets with this purchase!! | 电话通话麦克风效果等                       |
| 功能操作的易用性         | 199          | 70.85%   | amazing glasses, very easy to use and setup with just downloading the meta app | 易于设置和使用                             |
| 性价比                   | 190          | 60.53%   | Great product in great prices strongly recommended           | 价格与功能比                               |
| 重量与平衡               | 153          | 71.90%   | Love love will purchase more.Very lightweight and easy to travel with. | 重量分布，是否对鼻子和耳朵造成压力         |
| 充电便利性               | 153          | 70.59%   | I was on the fence about these glasses. By far the most expensive pair of glasses I own. Worth every penny. Sound quality is great, takes great video too. The battery's last about four or so hours with heavy use. Which is fine because they charge in about 30 minutes right in the supplies case. | 是否对充电方式满意，                       |
| 产品耐用性               | 129          | 47.29%   | This was a great buy. The glasses are very durable and the case ensures that I have a charge on my glasses every time I pick them up. There is Crystal clear reception on these glasses. The case is made of a durable plastic that not only charges but protects against hard drops, spills or tough contact. This was definitely a great purchase. | 如遇到连接问题和产品损坏                   |
| AI功能性的丰富程度       | 129          | 4.65%    | Compared to Siri, Meta is unable to identify song, play a requested song, locate current location (although it asks for permission to access location setting all the time). It’s also very slow to connect to the phone. Example, it wasn’t able to calculate a simple math problem until Bluetooth was connected. | AI功能性的局限性太强                       |
| 尺寸与调整性             | 128          | 62.50%   | they fit very well on my face ,not too heavy,as i expected, very well constructed, all other equitment on glasses works very well, im happy with my purchase of my glasses. | 对于尺寸设计的满意程度                     |
| 应用程序稳定性           | 117          | 45.29%   | These glasses are so amazing. The video quality is so clear and refined. It works with multiple apps that help download and track your car functions. This product is such an awesome idea, great technology, and super easy to use. Highly highly recommend | 如遇到应用冻结和连接问题                   |
| 配件可用性               | 97           | 42.27%   | I bought my glasses and charged them up. I paired the glasses to my IPhone, and was in awe with the sound quality I had using the Bluetooth feature on a call. Talking about, Hands Free!! BTW: I took the frame to a local eyeglass business and got my own lens put in to wear throughout the day. Use your Eyeglass Prescription to get yours in for a little of nothing if, available. | 如用户对对无法购买替换充电盒或镜片表示不满 |
| 款式选择多样性           | 75           | 84.00%   | These were perfect! Don’t be afraid to go with the green lenses they look black when worn outside too. 10/10 | 对现有款式选择的满意程度                   |
| 鼻托适配性               | 66           | 56.06%   | The low bridge fit is a game changer for me. I’ve never paid attention to bridge fit before. I would just pick a style I like and if it fits my head, I go with it. But with some of my glasses, they slip down my face, and I find myself often pushing them back up. With these Headliner low bridge fit sunglasses, I’ve never had to adjust them. They sit nice and comfortable on my nose. There are no adjustable silicone nose pads. It’s just the plastic frame that protrudes and acts as the nose pad. | 如适配性不佳，导致长时间佩戴不适           |
| 客户服务                 | 51           | 33.33%   | My glasses were everything I expected and more. The customer service was incredible as well there. I would recommend everyone to purchase a pair of Meta Ray Ban glasses. Overall satisfied! |                                            |
| AI稳定性与交互体验的问题 | 47           | 8.51%    | Overall they perform better than my expectations.  Cool classic looks is a big plus.  Sound quality is pretty clear and provides enough details.  Taking photos or videos is so effortless with the easy to reach button or voice prompt if your hands are tied up..  looking forward to AI model updates so it can perform better. | 用户界面和交互设计                         |
| 地区限制                 | 24           | 8.33%    | It works well but needs a US Apple ID to download the meta-view app. If you want to use the speaker on a bus or subway, sometimes you cannot hear anything from the speaker. But if you are using it in a mall or on the street it can give you a not-bad sound quality. | 在某些国家和地区，用户无法使用全部功能     |

数据分布如图所示：

![image-20241128142127510](D:\BDA-QAB\IS6335\FInal_project\分析视图.png)

用户好评主要集中在以下方面：

- Ray-Ban的播放音质
- 拍照便利性
- 外观设计
- 相机性能
- AI助手的便捷性和智能响应

用户差评主要集中在以下方面：

- AI功能性的丰富程度
- AI稳定性与交互体验的问题
- 地区限制等
- 续航时长

### 使用场景方面

在本节中，分析聚焦于在关于不同使用场景下的好评与差评

| 场景           | 评论总提及数 | 好评占比 | 实例                                                         | 说明                                                         |
| -------------- | ------------ | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 日常生活与娱乐 | 536          | 98.13%   | Brought these glasses for my husband who loves all thing tech, and they have lived up to there hype! The picture and video quality is top tier. Glasses are lightweight and stylish. | 在城市生活中使用，如行走时听音乐、视频通话，以及社交活动中分享体验，注重便利性和娱乐性 |
| 职场与专业环境 | 36           | 100%     | This device is well-suited for recording short product review videos or performing tasks while using both hands. It is also ideal for live streaming. However, it is unfortunate that it does not support streaming on platforms other than Facebook and Instagram. | 适用于会议、日常工作沟通，用户通过智能眼镜接听电话、使用语音命令，以提高工作效率 |
| 户外和运动场景 | 277          | 94.95%   | I was unable to get the transistion lenses to go dark when outside.  They were not sunglasses. Overall though they are amazing glasses and productive. I instead bought the dark lense ones. | 包括徒步、骑行、飞钓、滑雪等，用户利用智能眼镜进行拍照、听音乐，同时保持对环境的感知。 |

注：此处分析并没有具体分析在特定场景下的使用评价，仅给出了在提到此类场景时，用户是否给出了好评，而非作为给出好评的原因。

产品的主要应用场景在日常生活娱乐中，多数差评集中在户外和运动场景下。

而对于好评和差评的原因，请见上节。