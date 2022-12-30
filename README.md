# XR
协作者：Maggie 刘梦琦  包晨

<b>Key Word：</b> Pancake，硅基OLED/Mini LED，FOV，PPD，6DoF，光波导，See Through，Eye Tracking，注视点渲染

一、发展历史
---
技术萌芽（1968-2012）哈佛首台头戴显示设备。1990出现VR热潮，但算力不足
欲望膨胀（2012-2016）大批企业入局，2016VR元年，首台消费级Oculus眼镜
低谷（2016-2019）小厂商淡出大众视野，头部公司蓄力。谷歌推出虚拟现实纸盒Cardboard
复苏与发展（2019至今）头部厂商技术积累，步入元宇宙。VR+AR头显出货量有望突破1500w
与智能手机类比，当前XR发展期接近2003年智能手机，预计2030年左右迎来爆发点【图示】

![1](https://user-images.githubusercontent.com/118708553/210030569-4b088b53-c879-4548-92e3-34ac2d5c9544.PNG)


二、主流设备&发展程度
---
### 2.1 当前主流XR设备
VR：
华为VR Glass（分体式）
HTC Vive Focus 3
HTC Vive Pro 2
HTC Vive  Flow
爱奇艺奇遇3

AR：
MS hololens 2
Magic Leap 2
Google Glass
Nreal Air
雷鸟Air
Rokid Air（分体）
联想 ThinkReality A3（分体）
INMO Air

MR：
Pico4
Quest pro
Pico4和quest pro对比 

各设备详细参数：

https://zhuanlan.zhihu.com/p/99843981
https://docs.qq.com/sheet/DQmxMZHNPQ1ljWVBE?tab=BB08J2

![2](https://user-images.githubusercontent.com/118708553/210030681-615fd448-7e10-4c69-be73-45a7cfb9190f.PNG)


### 2.2 视觉标准--视觉图灵测试
现状：视觉是否通过图灵测试？没有
meta实验室构造的概念：视觉图灵测试，定义了VR显示器的4个特征，分别是

分辨率（resolution） 焦点（focus） 畸变（Distortions） HDR（高动态范围）

<b>分辨率</b>（后文提到）
<b>焦点深度（focal depth）：</b>通过verifocal和eye tracking来看任何距离的物品。当使用VR时，左右眼看到同一物体的不同角度，大脑根据看到的图像和诚一个富有立体感的物体。但是，目前所有的消费级VR头显，采用的都是定焦镜头，也就是说实际上在看一块很近的屏幕，且图像聚焦在固定的距离。使用者接受到的信息里缺乏深度信息，这就造成了视觉辐辏调节冲突。会带来视觉疲劳，诱发VR眩晕感，是VR重点难题之一。
Half Dome 原型机一直专注于解决这个问题（一堆液晶透镜层，每个透镜层施加电压，改变单个焦距）。Pico4与Oculus不同方案

<b>光学畸变</b>
球面失真，视野越大，图像越扭曲。

<div align=center>
<img src="https://user-images.githubusercontent.com/118708553/210030743-c2061508-c8cd-46bd-9d08-6315d4de28f2.PNG"/>
</div>
  
眼镜移动观察不同方向，虚拟图像畸变会变化，矫正困难，完美的矫正应该是动态的。Meta团队构建了一个失真模拟器，可以在不使用头显情况下研究不同光学设计和失真矫正算法。

<b>HDR：</b>
非常高的对比度能够显著提亮亮度，高亮度带来更高真实感。Starburst原型机（20000尼特）亮度是Quest 2的200倍。

三、如何获得良好的XR体验
---
目前的XR体验存在纸片化概念，用UI设计到交互都保留了2D的设计理念，更像2.5D体验。在XR交互中，搜索、选择等交互方式仍然采用2D平面方式（手机/pc）。而3D的交互方式应该摆脱纸片形式，实现用手操作，而不是用手柄或者鼠标键盘。
Quest 中应用 softspace AR在输出方式上做到了3D交互

【softspace AR视频https://www.bilibili.com/video/BV1RL4y1N74L/?spm_id_from=333.337.search-card.all.click&vd_source=42111033a8fc854e50b52160b9095f76】

### 3.1 精准的空间定位
- DOF：从3dof→6dof，自由度越高，能够识别的动作维度越高
  - DoF自由度：3DoF代表三维空间中的三个自由度，即沿x、y、z轴的位移。6DoF代表六个自由度，包括前面的三个自由度和三个旋转角，即沿着x、y、z轴的旋转。（总结：位移+旋转）

<div align=center>
<img src="https://user-images.githubusercontent.com/118708553/210030790-82645a2c-b548-4dba-8ada-456f1a227ac8.png"/>
</div>

- 3DoF：只能检测位移
  - 手部（手柄）：只有三轴旋转功能，显示射线指针
  - 头部（头显）：射线投射
  
<div align=center>
<img src="https://user-images.githubusercontent.com/118708553/210030828-41ca1027-2a2d-43c6-9960-e6f7a396842a.png"/>
<img src="https://user-images.githubusercontent.com/118708553/210030844-5241504f-9a92-49d4-bcd6-f63e11082605.png"/>
</div>

- 6Dof：检测头部转动带来的视野角度变化外，还能够检测身体移动带来的旋转变化
  - 头部
    - 解决方案：
      - Outside-in：非目前主流方案，外部定位器+头部追踪，易产生校准偏差、校准过程繁琐
      - Inside-out：目前主流方案，头显内的摄像头标定头显位置
        - SLAM技术：重复观测环境特征定位自身，再根据自身定位构建环境，达到同时定位及地图构建
  - see through 解决方案：(https://blog.csdn.net/S_DreamLab/article/details/123332170)
    - 光学透视OST（AR方案）：和眼镜相似，直接看到现实世界。光学模组并不是完全透明，由此通过真实图像叠加虚拟图像来实现AR现实。缺点是难以显示黑色和深色，阴影渲染很困难。常见方案有光波导（Magic Leap）和半反半透。
    - 分辨率高，不易晕屏
    - 光波导优势：较小的机身体积；劣势：图像质量存在问题，FOV小，光学效率低，对微显示屏的要求较高，需要配合LCos和Micro OLED显示屏，成本高
    - 半透半反：设计起来更复杂，但成本远低于光波导方案
    - 【AR光学：https://zhuanlan.zhihu.com/p/78487566】
    
![7](https://user-images.githubusercontent.com/118708553/210030867-41c55fa3-2e75-4b56-9512-94129a131418.png)

  - 视频透视VST（VR方案）：相机捕捉实时视图结合计算机图像技术，显示器不透明；头显重量、体积方面有较大局限
    - 更容易实现遮挡（MR需要）
    - FOV更大
    - 虚拟与真实的延迟更容易匹配
  - 设备举例：
    - Pico 4：VST方案，引入彩色RGB摄像头提供彩色透视效果。把外置彩色RGB摄像头获取的画面完整传输到眼镜上，再通过4角鱼眼相机扭曲平面图像，稍微带一点深度信息。清晰度很高，距离感较差。
    - Quest Pro：VST方案，两颗摄像头黑白透视，一颗彩色摄像头实现彩色透视。用两颗前视的黑白摄像头构建双目点云信息，然后用中间1600w摄像头，然后把它切分成很细很细的一个个小的彩色贴图，贴在这一个个本身有深度信息的点上面。然后呢这样构建出来的 VX 做这个画面形态就会有非常强的深度感，因为它本身就是基于深度贴图去完成这个画面贴图传输。
  - 手部：去按键化，采用了更多手指感应方案
  
### 3.2 3D体验感——不眩晕&真实的渲染
- 画面不畸变
- 延时:处理器
  - 算力解决方案：
    - 头显内置芯片（算力在头显设备内部）：提升高品质体验需突破的关键点
      - 高通：
        - 目前市场上的主流设备都是使用的高通骁龙XR2芯片
        - 今年10月12日发布了AR/VR芯片骁龙XR2+ Gen1，续航较上一代提升了50%，散热提升30%，外形尺寸更小更轻Oculus Quest Pro首发骁龙XR2+芯片（2022年10月发布）
        - 今年11月17日发布了专为AR的骁龙AR2平台，相对XR2整体功耗降低50%，AI性能提高2.5倍
        
<div align=center>
<img src="https://user-images.githubusercontent.com/118708553/210031029-787ff1de-418b-446f-bab1-5c1e07a4bc00.png"/>
<img src="https://user-images.githubusercontent.com/118708553/210031041-677b8f4a-e5f6-4a80-9b48-5ac9ca0916f3.png"/>
</div>

      - 现状：
        - 中高端XR芯片仍被海外厂商占领，国内厂商目前在芯片设计和算法支持上仍有较大差距
        - XR芯片投融资从2020年起火爆，VC（红杉、纪源、高榕、启明创投）和CVC（腾讯、字节、美团）均做布局
       
![10](https://user-images.githubusercontent.com/118708553/210031107-d340667d-8651-4ab0-b163-2cb62af3b455.png)

    - PC串流（算力转移至电脑）：通过数据线链接将一体机变为PC VR
      - 优点：可用内容大大拓展，头显设备限制下降
      - 缺点：会受到数据线的束缚
    - 5G网络（云边端，算力转移至云）--云化XR 智终端、宽管道、云应用
      云化XR又称CloudXR，是将物理硬件迁移至云端/边缘端，使得轻量级终端只保留呈现XR最基本的功能。
        - 5G赋能云XR：
        5G高速率、低延时，可以为设备提供1Gbps传输速率，使得我们能够实现在较低延迟的情况下，在云端计算渲染后，将内容快速传输至XR终端。
        基站广布，为边缘计算提供更多可能，减少内容汇聚，降低时延。
        - CloudXR解决方案：
        CloudVR基本准则是将消耗资源的计算转移到云或边缘端，并将内容通过低延迟高宽带5G网络传输到轻量级客户端。CloudAR：需要实时理解并适应现实世界的场景，需要额外的传感器，场景识别和计算功能。带来好处：轻量级客户成为可能的发展趋势，移动性更强，电池寿命更长
        【云架构分为两层。中心节点负责5G网络控制面功能和管理平面功能，边缘节点负责用户平面功能和边缘计算平台功能。下图为CloudXR网络架构和延迟。
      
<div align=center>
<img src="https://user-images.githubusercontent.com/118708553/210031115-a4d523ee-0eef-4494-b31a-cdbbcf1a556b.png"/>
</div>


        - Cloud XR5个不同阶段：
          - Wireless X labs提出了5个阶段定义Cloud XR演进过程。目前处于第二阶段。
        
<div align=center>
<img src="hhttps://user-images.githubusercontent.com/118708553/210031126-d123e4cb-5fad-4eee-a356-8dfa8cab299e.png"/>
</div>

        - CloudXR关键技术
          - 1.FOV视频传输
          - 2.端云异步渲染
          - 3.低延迟编解码优化
          - 4.网络切片
        - CloudXR挑战：
          - 1.XR本身技术成熟度：光波导、空间场定位、tof、近场通讯、眼球追踪
          - 2.5G网络大规模普及存在挑战
          - 3.CloudXR对于时延要求较高，需要对网络升级，运营商面临如何以较低成本实现高质量时延的挑战
          - 4.生态不健全：运营商 平台 内容 终端多个角色健康生态环境以及共赢商业模式；平台和系统间的互联互通
          - 思考
          - 1）怎样能在云端保持低延时的情况下产生这些内容（目前仍有20-30毫秒的延时）
          - 2）怎样保证无限输出的情况下把这些内容发送到用户屏幕上
          - 【Nvidia CloudXR https://www.bilibili.com/video/BV1AB4y1B7oD/?spm_id_from=333.337.search-card.all.click】
- FOV 人眼横向FOV220度
  - 当前VR设备可达视场角90-120°（QuestPro 106，Pico4 105） 
  - AR设备光学方案仍面临视场角问题（约50°）
  - AR光学方案主要有离轴反射（RealMax，DreamGlass，LeapMotion）、BirdBath（联想Mirage，Neral），光波导（Hololens，MagicLeap）。理论上光波导技术兼具大FOV，小体积，高透光率，高清画质特性，在长期是AR的理想解决方案。但目前仍存在视场角过小问题。
  - 其中表面浮雕光栅波导（SRG）技术已被Magic Leap证明在经济成本上是可行的，虽然光效降低，但AR厂商已经转向高亮度的硅基 Micro LED（LEDoS）来解决这个问题。
- 清晰度：分辨率、刷新率、PPD、IPD
  - 分辨率：VR头像屏幕像素点数量。分辨率单眼4K/8K清晰度较好，市面上单眼2K为主
  - 刷新率（影响图形稳定）：理想刷新率180HZ，现有VR头显70-120HZ
  - PPD：pixel per degree，角分辨率，指视场角中的平均每 1° 夹角内填充的像素点的数量。人眼正常视力下的分辨能力极限约为 50 ~ 60 PPD （视网膜级别 PPD）。PPD 越小，晶格感越强烈（纱窗效应）。PPD指标对于清晰度的描述不会受到凝视点位置的影响。人眼对于凝视点较远的地方，分辨能力较弱，对于凝视点的分辨能力很强。PPD60的概念是不论屏幕距离我有多远，在什么位置，我都分辨不出像素。
  - 现有的渲染能力无法达到PPD60，目前市面上头显仅能达到20。解决方案：forveated rendering 注视点渲染&eye tracking。目前quest正在做注视点渲染压缩，下图为英伟达的forveated rendering效果图。英伟达在注视点渲染方面有两个技术VRS（variable rate shading） 和VRSS （variable rate super sampling）
    - 【VRS:https://learn.microsoft.com/zh-cn/windows/win32/direct3d12/vrs】
    - 【VRSS: https://zhuanlan.zhihu.com/p/104354378】
    - 【Varjo（PCVR） https://developer.varjo.com/docs/native/foveated-rendering-api】
    
![13](https://user-images.githubusercontent.com/118708553/210031137-949b88db-904f-49ae-bd01-e217bd85db7f.png)


- IPD 瞳距：
  - 如果镜片的光学中心和瞳孔没有正确对齐，使用者将会看到模糊的画面，处理不当还会导致头疼和晕眩
  - 分类：
    - 硬瞳距：直接调节VR镜头之间的物理距离位置，结构更复杂，成本和重量更高
    - 软瞳距：VR镜头物理位置固定不能调，但因为瞳距对准允许一定误差，设备光学设计时会可以增加允许误差范围，调整渲染参数来适配不同瞳距，可调范围较小，结构简单，成本较低
  - 当前主流解决方案：
    - 手动调节：Pico 4方案，62-72mm电动无极调节，通过手柄实现
    - 自动调节：有眼动追踪功能的设备可以实现，Quest Pro 58-72mm自动调节
  - 现状：
    - 大部分主流设备支持硬瞳距调节
    - 部分较早期设备为固定瞳距
    
### 3.3 精确地调整交互
- 语音交互：
  - 双麦克风阵列降噪
  - 三麦克风阵列降噪
  - 增加语音识别库
- 手柄：pico 4 和 quest pro对比
  - 手势交互：通过操作手柄（6DoF）
  - 触觉反馈：主要是按钮和震动反馈
- 虚拟动捕：
  - 动捕：使虚拟角色拥有真人角色的数字栾生
  - 技术方案：常用惯性导航式、光学式两种方式
  
![14](https://user-images.githubusercontent.com/118708553/210031146-318507c5-c117-4059-8f88-3e9b312db4e7.png)

  - 技术：
    - 激光定位技术：空间内安装发射激光装置，被定位物体安装激光感应接收器
      - 代表：HTC Vive——Lighthouse定位技术，靠激光和光敏传感器来确定，手柄和头显上有70个光敏传感器
      
<div align=center>
<img src="https://user-images.githubusercontent.com/118708553/210031153-d0437c8c-9dca-4f44-9dcc-7ec009f40d40.png"/>
</div>



    - 红外光定位技术：空间内安装红外发射摄像头，被定位物体安装红外反光点，摄像头捕捉反光
      - 代表：Oculus Rift——主动式红外光学定位技术+九轴定位系统
        - 主动式红外光学定位：头显和设备发出红光，外部两台摄像机接受红光计算后得到空间坐标
        - 九轴传感器在红外光学失灵时发挥作用
        - 使用范围由于摄像头视角限制仅为1.5m*1.5m
    - 可见光定位技术代表：原理与红外光相同，但换成可见光
      - 代表：索尼PS VR
    - 计算机视觉动作捕捉技术：用高速相机从不同角度对运动目标进行拍摄，再用程序计算
      - 代表：Leap MoTIon手势识别技术——VR头显装两个摄像头获取手势捕捉
    - 惯性传感器动捕技术：被定为目标佩戴惯性传感设备，采集运动信息
      - 代表：诺亦腾 - PercepTIon Neuron
      
<div aign=center>
<img src="https://user-images.githubusercontent.com/118708553/210031167-7315b271-24d2-49e3-b0ab-3260196662f5.png"/>
</div>


    - 头显解决方案：通过AI训练后的预测功能，利用头显获取的身体一部分的动作（比如上半身）预测全身动作
      - 代表：meta九月发布论文提出了一种仅通过Quest实现全身动捕的解决方案（无需光学标记），VR头显从仅可以实现面部表情捕捉到全身动作捕捉。
- 眼球追踪：
  - 价值：
    - 眼动控制实现交互增强，降低手柄使用，解放双手
    - 推动实现注视点渲染，降低CPU算力和功耗，同时人眼体验更真实
    - 融合光学模组减少眩晕感解决晕动症
    - 眼动数据分析描绘用户画像
  - 现状：
    - 大厂研发专利+并购入局（三星注资FOVE主打眼球追踪VR头盔、Google收购Eyefluence、Oculus收购The Eye Tribe、蚂蚁金服收购EyeVerity、苹果收购SMI打造眼球追踪AR）
    
![17](https://user-images.githubusercontent.com/118708553/210031173-8f8e34c3-6df3-492d-b2c1-dd92fe4410b6.png)

    - 品牌厂微软、Meta、Pico、Magic Leap、HTC、创维、小派、Varjo、Gear 等均已推出支持眼球追踪的XR设备；索尼、苹果等搭载眼球追踪功能的消费级新品即将上市
  - 技术实现：
<div align=center>
<img src="https://user-images.githubusercontent.com/118708553/210031181-245860bb-d574-4040-95c6-efeed6ae4f53.png"/>
</div>


- 脑机接口：依赖于硬件层（脑电采集设备、外控设备）和软件层（生物信号分析、核心算法、通信计算和安全隐私）的技术突破，目前在XR设备上没有特别落地的应用，但在医学领域有一些尝试https://zhuanlan.zhihu.com/p/372360870

### 3.4 头戴式体验
- 重量：受光路设计、屏幕尺寸以及诸多传感器件的限制，500克左右的重量和厚重的体积似乎成为VR头显一道难以跨越的坎，鲜见VR硬件制造商取得大幅的突破。Pico 4（586克）、Quest Pro（722g）Oculus Rift S（500g克）、HTC VIVE（470克）、HP Reverb G2（550克）。而理想的重量是300g。
  - 解决方案：Pancake光学方案+硅基OLED/Mini LED/Micro LED显示屏。当前Pancake方案已经在VR设备中开始广泛应用；硅基OLED在大部分AR眼镜中已应用，但VR设备仍采用Fast LCD，长期来看Micro LED是最优方案。
  
![19](https://user-images.githubusercontent.com/118708553/210031194-d8c65607-53b6-433c-888c-76f47969ceb2.png)


  - Arpara可实现380g，价格6000-7000rmb【Arpara http://www.yitb.com/article-19259】
- 电池寿命：目前的VR头显的电池寿命较短，需要经常充电，pico4与Quest Pro续航均不到2小时。
  - 解决方案：XR的专用芯片，专门配合XR的渲染场景
- 屈光度调节
- 方案：
  - 头显设备内部预留一定位置配戴眼镜
  - Alvarez变焦系统：光学架构解决方案，镜片厚度不一，调整两个镜片重叠部分

<div align=center>
<img src="https://user-images.githubusercontent.com/118708553/210031204-ffe5e7b1-7430-4def-82e8-e763d5a7f993.png"/>
</div>

 - 液体透镜+可移动显示屏（改变液体透镜形状，如通过电压）

![21](https://user-images.githubusercontent.com/118708553/210032028-8dfc1a7b-7d44-4d1c-b019-7042542fe6c7.png)



- VR和AR的不同：
  - VR：只需针对虚拟像面调节屈光度，因此可直接调节成像镜头
  - AR：需要同时针对虚拟场景和真实场景，需要同时调节成像镜头和入眼介质
- 现状
  - 部分中高端VR眼镜配备了屈光度调节方案，但仅针对轻度近、远视需求，0-600度
  
### 3.5.丰富的内容产出&3D UI设计
- 当前模式：买断制为主，订阅制并存
- 主要应用场景
  - 游戏：国内外差距大。国内VR游戏不论从数量和质量都不能和国外抗衡。
    数量上，Quest 商店游戏数量约为360款，加上非官方应用商店Side Quest，远高于Pico商店的280多款。游戏知名度上，Pico 4此次主要上新了6款游戏，分别是剑与魔法、玩命特效、Espire1、阿尔沃行动、城市叠叠乐、白夜传承，虽然相比Pico 3已经有了显著进步，但这几款游戏在知名度上远不及Quest Pro。同期Quest新上线的游戏囊括了很多大IP，包括漫威系列下的钢铁侠、曾一度爆火的狼人杀游戏Among us，行尸走肉第二章等。
  - 健身：多家竞争，生态较为成熟。PCVR发展到一体机，菲涅尔透镜发展到Pancake方案，头显轻量化，降低VR健身门槛。更高精度的定位、追踪和交互技术，使得VR中运动体验感得到提升。
    健身应用两个方向：趣味健身（Beat Saber，Just Dance）+专业健身（莱美搏击，超燃一刻）。Pico推出50多款健身应用，主要方式为自研+引进，涵盖健身房内所有运动与课程，与帕梅拉等健身达人推出私教课；Quest收购头部工作室，已收购Beat Dancer，有意收购Supernatural，但遭到反垄断诉讼。
  - 直播：字节老本行，Pico视频当前表现出色，以周为单位高效迭代。抖音视频，世界杯直播间，虚拟偶像演唱会
  - 生产力：VR生态目前缺陷，各大厂布局方向。目前的生产力软件主要面对B端，但长期来看会向C端发展。Meta已与MS达成深度合作，旗下的Teams、Office、Windows将全部引入Quest头显；Autodesk正在更新其协作程序，从而适配Quest Pro新功能，为建筑师和设计师提供沉浸式查看3D模型的全新方式；Adobe表示，面向专业的3D建模师、设计师和艺术家开发的substance 3D应用，将于2023登录Quest Pro。我们的校友：Presence XR 全息演示。本季申请项目：MetaTelling 3DPPT编辑器。
- 应用体验VR游戏、应用体验记录 （From Allen）

四、 产业链
---
XR产业链 

![22](https://user-images.githubusercontent.com/118708553/210032043-71bff547-11d2-40e8-9fbe-07a7b2e2a224.png)



五、机会
---

![23](https://user-images.githubusercontent.com/118708553/210032075-390a80a3-f531-4167-9548-82004a097509.png)


- 生态：
UI设计，AIGC，办公，教育，医学，心理
- 技术突破：
云边端，延时降低，大游戏可能性，AIGC
- 硬件BOM成本
光学 显示 摄像头模组领域价值量占比提升。
Pico4 BOM成本348.255美元，综合硬件成本约368.25美元，税后成本约为2913元。
两块Fast-LCD屏幕84美元，成本接近1/4，SOC高通骁龙XR2芯片60美元，占16%，光学模组成本44美元，占12%。综合硬件成本按照供应链厂商分，JDI/群创作为屏幕供应商价值量84美元，占比23%；歌尔作为光学声学模组供应商，价值76美元，占比21%（Pancake成本上升8倍）。高通作为芯片提供商价值65.2美元，占比18%，XR2价格出现一定下降。按供应链国别看，国产供应商125美元，35%，海外242.6美元，65%


- 交互形态：
眼动/面部，手指，嗅觉【气味王国】，味觉
- Forecast
苹果MR【苹果分析师郭明琪连发8条推特】

![24](https://user-images.githubusercontent.com/118708553/210032090-e8b4985f-44d8-43bd-b620-3488efe62bfb.png)

已知供货商：大立光（镜头）、玉晶光（Pancake）、高伟电子（相机模组）、致伸（眼动追踪模组）
其他爆料：苹果头显将由和硕独家代工；第二代头显将由3p Pancake透镜；正与台积电联合开发XR芯片；蓝思科技将成为苹果XR头显玻璃、金属的核心供应商
预测时间：2023年底。MR头显零部件大量出货时间可能是2023第二季度。苹果MR头显操作系统“realityOS”开发正在内部收尾（彭博社）。
出货量：预估低于50w台
预测价格：$900-$3000。我的观点：$1500-$2000

PS VR2; Quest 3
QA：
1.inside-out目前采用slam技术，中间有惯导零漂问题，目前解决程度到什么样了？
2.我交流过一个教授，说眩晕感来源有三个层面，一个是延时，一个是视场聚焦，还有一个是大脑反馈跟身体反馈不协同(大脑认为自己到那里，但是身体没有到那里)，第三个问题是很难解决的根本问题，想问一下有没有了解过这一块？


随堂补充：目前的5G 在2023年能做到 一线城市走到大街上 电信 移动 20-30ms的延时。为了把云 边 端 协同进一步提升，移动也在尝试自己提供边缘算力，但是想支持整个生态 可能还不够。
随堂补充：边 和 端 如果不用线 最近也看到了毫米波链接的方式。
