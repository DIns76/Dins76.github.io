---
title: 这几天想做的事
date: 2020-4-25
tags: [FreeRTOS, VScode, vim, gcc-none-eabi-arm, Android_studio]
hide: true
---

这近十天里，真正发现自己全都乱了！
1. 首先，最重要的是生物钟完全混乱；这个是以前暑假就会改成日夜颠倒，当时并没有觉得会有什么，因为一直想的是，没有什么时候或者地方能比凌晨这段时间安静了。还自以为真的能让自己静下来，结果什么有用的事情都没做，白白的全浪费了，现在真的顿感可惜、可笑、可恨。
2. 再就自然是什么事情都没做成，要不然心里直接就拒绝开始；心里也一直乱糟糟的、自己也可以感觉得到的烦躁（浮躁？？）
3. 再就导致现在开始一件事，就直接集中不了精力，久而久之就丧失了耐心
4. 现在就是躺床上，脑中也是不断有想法冒出，直接造成了睡得更完了；

这一整个都自己形成了一个恶行循环闭环/(ㄒoㄒ)/~~

上篇落下的还没做不说，就是今天想做的也嫌麻烦，什么也没做成；本来想：
- 最开始在``f103C8``用``FreeRTOS``来闪个板载灯，入个门；本来也就有``Keil``的``Demo``，想来直接用``keil``打开编译通过，才好进入下一步的；结果编译就是没通过，错误信息一搜，居然是``license``有问题，导致有编译字节限制😓开``管理员权限``还是没能解决，所以暂时放下了。
	- 下次尝试使用开源的工具链，也搜了下，找到一篇较新的文章:[F103C8T6 HAL库 Makefile FreeRTOS 工程模板](https://www.cnblogs.com/Luad/p/12635149.html);通读下来，工具使用确实很轻量：``VSCode + GCC工具链 + OpenOCD``；但发现比较关键的是没在``FreeRTOS``源文件里找到编译用的``Makefile``，而且找``F103``和``GCC``相关的文件也是要和特定``IDE``才能用的 (lll￢ω￢)
- 然后想``Android studio``放了太久，应该继续熟悉，结果一打开就要更新，更到现在，而且拖累得电脑反应要好几秒；我现在才记起来：``Android studio``之所以放了这么久，就是因为我的电脑反应已经跟不上了，随意打个单词都要一个字母一个字母的反应😶

现在最应该仔细想想**最初是如何步入这个困境的**，后续对解决方法或许会有启发

参考链接：
- [Modifying a FreeRTOS Demo](https://www.freertos.org/porting-a-freertos-demo-to-different-hardware.html)
- [FreeRTOS Kernel Quick Start Guide](https://www.freertos.org/FreeRTOS-quick-start-guide.html)
	- 暂时因为``license``和``Makefile``的问题，卡在**Building the project**
- [Mastering the FreeRTOS™ Real Time Kernel](https://www.freertos.org/wp-content/uploads/2018/07/161204_Mastering_the_FreeRTOS_Real_Time_Kernel-A_Hands-On_Tutorial_Guide.pdf)
- [FreeRTOS在Cortex-M3上的移植](https://blog.csdn.net/zhzht19861011/article/details/50072033)
- [编写优质嵌入式C程序](https://blog.csdn.net/zhzht19861011/article/details/45508029)
