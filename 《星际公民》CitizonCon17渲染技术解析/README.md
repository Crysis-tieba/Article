大体渲染流程没太多可说的，和其他游戏都差不多，生成一张全局cubemap->depth pre pass->生成gBuffer->光照，然后就是些复杂材质啊，SSR，froxel体积光，后处理的什么的

几个亮点：
![alt text](https://raw.githubusercontent.com/Crysis-tieba/Article/master/%E3%80%8A%E6%98%9F%E9%99%85%E5%85%AC%E6%B0%91%E3%80%8BCitizonCon17%E6%B8%B2%E6%9F%93%E6%8A%80%E6%9C%AF%E8%A7%A3%E6%9E%90/img/1.JPG)
![alt text](https://raw.githubusercontent.com/Crysis-tieba/Article/master/%E3%80%8A%E6%98%9F%E9%99%85%E5%85%AC%E6%B0%91%E3%80%8BCitizonCon17%E6%B8%B2%E6%9F%93%E6%8A%80%E6%9C%AF%E8%A7%A3%E6%9E%90/img/2.JPG)
-法兰克福分部写了个新的SSDO方法，有一个专门的pass会计算ssdo需要用到的bent normal以及每个像素的遮挡cone的角度  
-计算HDR的曝光范围时，会生成一个直方图来计算，而不是传统的计算全屏平均亮度来完成  
-tonemapping换用ACES curve
![alt text](https://raw.githubusercontent.com/Crysis-tieba/Article/master/%E3%80%8A%E6%98%9F%E9%99%85%E5%85%AC%E6%B0%91%E3%80%8BCitizonCon17%E6%B8%B2%E6%9F%93%E6%8A%80%E6%9C%AF%E8%A7%A3%E6%9E%90/img/4.JPG)
-基于物理的玻璃材质，支持基于物理的反射、折射，以及一个薄膜干涉效果的近似（目测是Unity的方法）  
-抗锯齿方法：TAA+SMAA，TAA的实现似乎和主流方法不一样，主流方法是把每一帧都blend进一个accumulation  buffer，星际公民的则是往前读4帧来拿到之前的信息。  
-shadowmap是5个cascade，用一个mask来标记不同光源的阴影  
![alt text](https://raw.githubusercontent.com/Crysis-tieba/Article/master/%E3%80%8A%E6%98%9F%E9%99%85%E5%85%AC%E6%B0%91%E3%80%8BCitizonCon17%E6%B8%B2%E6%9F%93%E6%8A%80%E6%9C%AF%E8%A7%A3%E6%9E%90/img/3.JPG)
-有个渲染的大气的pass，Ali Brown说会用来预计算一些大气效果给后面用，没听明白是干嘛的  

随后介绍了些I/O，多线程方面的优化，没细听  

最后画了几个饼，星球阴影，动态全局光照，大范围的星云效果体渲染，Vulkan支持  

最后，不明白为何要给普通玩家讲这个……看到介绍TAA前感觉台下已经睡了一大片了。  