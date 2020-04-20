## PaddlePaddle深度学习7日入门CV篇|Summaries

![avatar](https://mmbiz.qpic.cn/mmbiz_png/sKia1FKFiafgiaBaU5cOeECbUSWtmlQCqicImM2Lb1fk5GhEkYmjyHeAARE7xhKNgBl6pwd0V2RX1la3k1nVbgPhibg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)





[TOC]



## 一、<font color=#B2DFEE>什么是PaddleX？</font>

依托飞桨开源深度学习框架和丰富的工具组件，PaddleX进行全流程的整合打通，为开发者提供飞桨全流程开发的最佳实践。它集飞桨核心框架、模型库、工具及组件等深度学习开发所需全部能力于一身，提供简明易懂的Python API，方便用户根据实际生产需求进行直接调用或二次开发，是提升深度学习项目开发效率的最佳辅助工具。





## 二、为什么要参加训练营

1. 由于一只蝙蝠，带来了漫长的网课，老师布置的任务时多时少，而自己在完成老师规定的任务后时间还比较充裕，想着不如来打卡营学习，提升一下自己
2. 由于自己前期有在学习**python**，训练营的内容与所学也挺配，算是一种在python编程上的进阶吧
3. 为以后参加人工智能比赛做准备，同时也对自己玩树莓派比较有帮助





## 三、训练营都学些什么

### Day01 丁香园数据可视化

![avatar](https://ai-studio-static-online.cdn.bcebos.com/3ca5fa8e7019498ab7217aea7a552f0394ff092045174b9284920dbee57b0c1a)

![avatar](https://ai-studio-static-online.cdn.bcebos.com/28000edb58d34e2e991b6dc2739007ae837b9b031d8842528c9d9506941fbd17)



### Day02 手势识别

<img src="https://tse1-mm.cn.bing.net/th/id/OIP.dS_KgpkP2weqKYrNIxsiuwHaBj?w=290&amp;h=68&amp;c=7&amp;o=5&amp;dpr=1.25&amp;pid=1.7" alt="手势识别" style="zoom:150%;" />



### Day03 车牌识别

![车牌识别](C:\Users\86177\Desktop\车牌识别.png)



### Day04 口罩识别

![avatar](https://tse1-mm.cn.bing.net/th/id/OIP.hDpM6hXYP_RsxJPZgmqfYAHaD2?w=300&h=156&c=7&o=5&dpr=1.25&pid=1.7)



### Day05 Paddle hub 初体验

利用Paddle hub进行口罩识别

![trainning loss](C:\Users\86177\Desktop\trainning loss.png)

![trainning acc](C:\Users\86177\Desktop\trainning acc.png)

（改了好久，最后准确率还是崩了😭😭）

**以及**

**==人流密度检测比赛！！！==**

![avatar](https://tse4-mm.cn.bing.net/th/id/OIP.LdHI1VqPDtGGD7ZUMvBgsQHaGx?w=159&h=160&c=7&o=5&dpr=1.25&pid=1.7)

![avatar](https://tse1-mm.cn.bing.net/th/id/OIP.GiVWXe0JwmrWft-SHlsIaAHaEE?w=291&h=160&c=7&o=5&dpr=1.25&pid=1.7)

数据种类来源多样，采用框选和头部标点进行数据统计

采用*使用高斯滤波变换生成密度图*

```python
# 使用高斯滤波变换生成密度图
def gaussian_filter_density(gt):
    #Generates a density map using Gaussian filter transformation
    # 初始化密度图
    density = np.zeros(gt.shape, dtype=np.float32)
    
    # 获取gt中不为0的元素的个数
    gt_count = np.count_nonzero(gt)
    
    # 如果gt全为0，就返回全0的密度图
    if gt_count == 0:
        return density

    # FInd out the K nearest neighbours using a KDTree
    
    pts = np.array(list(zip(np.nonzero(gt)[1].ravel(), np.nonzero(gt)[0].ravel())))
    
    # if gt_count > 0 and gt_count < 20: 
    
    # leafsize = 2048

    # # build kdtree
    # tree = scipy.spatial.KDTree(pts.copy(), leafsize=leafsize)

    # query kdtree
    # distances, locations = tree.query(pts, k=4)

    for i, pt in enumerate(pts):
        pt2d = np.zeros(gt.shape, dtype=np.float32)
        pt2d[pt[1],pt[0]] = 1.
        if gt_count > 1:
            # sigma = (distances[i][1]+distances[i][2]+distances[i][3])*0.1
            sigma = 25
        else:
            sigma = np.average(np.array(gt.shape))/2./2. #case: 1 point
        
        #Convolve with the gaussian filter
        
        density += scipy.ndimage.filters.gaussian_filter(pt2d, sigma, mode='constant')

    return density
```



进行网络配置（可以采用VGG-16 卷积神经网络）

```python
def crowd_deconv_without_bn(img):
    x = img

    x = fluid.layers.conv2d(input=x, num_filters=64, filter_size=3, padding=1, act='relu')
    x = fluid.layers.batch_norm(input=x, act='relu')
    x = fluid.layers.conv2d(input=x, num_filters=64, filter_size=3, padding=1, act='relu')  
    print('3-64-2',x.shape)
    x = fluid.layers.pool2d(input=x, pool_size=2, pool_stride=2)  
    x = fluid.layers.dropout(x=x, dropout_prob=0.25)
    print('pool',x.shape)

    x = fluid.layers.conv2d(input=x, num_filters=128, filter_size=3, padding=1, act=None)  
    x = fluid.layers.batch_norm(input=x, act='relu')
    x = fluid.layers.conv2d(input=x, num_filters=128, filter_size=3, padding=1, act='relu') 
    print('3-128-2',x.shape)
    x = fluid.layers.pool2d(input=x, pool_size=2, pool_stride=2) 
    x = fluid.layers.dropout(x=x, dropout_prob=0.25)
    
    x = fluid.layers.conv2d(input=x, num_filters=256, filter_size=3, padding=1, act='relu') 
    x = fluid.layers.batch_norm(input=x, act='relu')
    x = fluid.layers.conv2d(input=x, num_filters=256, filter_size=3, padding=1, act=None) 
    x = fluid.layers.batch_norm(input=x, act='relu')
    x = fluid.layers.conv2d(input=x, num_filters=256, filter_size=3, padding=1, act='relu')  
    print('3-256-3',x.shape)
    x = fluid.layers.pool2d(input=x, pool_size=2, pool_stride=2)  
    x = fluid.layers.dropout(x=x, dropout_prob=0.5)
    
    # x = fluid.layers.conv2d(input=x, num_filters=512, filter_size=3, padding=1, act='relu')  
    # x = fluid.layers.conv2d(input=x, num_filters=512, filter_size=3, padding=1, act='relu')  
    # x = fluid.layers.conv2d(input=x, num_filters=512, filter_size=3, padding=1,act='relu' )  
    
    # x = fluid.layers.pool2d(input=x, pool_size=3, pool_stride=1, pool_padding=1) 
    # x = fluid.layers.pool2d(input=x, pool_size=2, pool_stride=2) 
    # x = fluid.layers.dropout(x=x, dropout_prob=0.5)

    x = fluid.layers.conv2d(input=x, num_filters=512, filter_size=3, padding=1, act='relu') 
    x = fluid.layers.dropout(x=x, dropout_prob=0.5)
    x = fluid.layers.conv2d(input=x, num_filters=512, filter_size=3, padding=1, act='relu') 
    x = fluid.layers.dropout(x=x, dropout_prob=0.5)
    x = fluid.layers.conv2d(input=x, num_filters=512, filter_size=3, padding=1)  
    x = fluid.layers.batch_norm(input=x, act=None)
    print('3-512-3',x.shape)
    # x = fluid.layers.pool2d(input=x, pool_size=3, pool_stride=2, pool_padding=1)  
    # x = fluid.layers.dropout(x=x, dropout_prob=0.5) 
    print('clowd_net output shape:',x.shape)

    return x
```

后面就是**模型训练**（基本上耗时最长的部分）、模型校验、**参数调整**（对于笔者这个小白来说最重要的）

<u>*俗话说，调参错，出出错（一个卷积核shape错误，或者一组权重错误，都可能导致你训练一上午的模型面临过拟合，甚至“瘫痪”）*</u>



### Day06 paddleslim模型压缩

![paddleslim模型压缩](C:\Users\86177\Desktop\paddleslim模型压缩.png)

### Day07 结营，公布比赛获奖名单，看大佬讲解模型

![avatar](https://tse4-mm.cn.bing.net/th/id/OIP.jVQ7XRqFarjYDw1WCMfgIgAAAA?w=125&h=166&c=7&o=5&dpr=1.25&pid=1.7)

![avatar](https://tse4-mm.cn.bing.net/th/id/OIP.ONPMIAXtnUT966k5SU7fiwHaE6?w=300&h=195&c=7&o=5&dpr=1.25&pid=1.7)





## 四、在训练营打卡的感受

1. 群里的小伙伴（有部分也不能称作小伙伴，毕竟都工作了😂）超级积极，学习氛围浓厚。有一位跟笔者经常讨论的大佬（前30名，笔者菜鸡0.2的错误率从78被挤到100开外）有一次通宵跑模型训练，一连工作15个小时
2. 另一方面来说，也是蛮累的，毕竟是在挤时间来调参、训练模型，gpu环境得要算力卡才能用，只有在晚上22：00后才可能抢得到gpu环境，不少老哥都是早上5点起床抢（有一说一，gpu上跑起来真的比cpu环境块多了，飞一般的感觉😍😍）
3. 群主和老师真的也很负责，批改作业，回答问题，不厌其烦，有时候班班也会用微信机器人的脚本
4. 难度有点大，对于小白来说不容易，各种vgg、cnn模型，全连接网络、神经卷积网络、各种优化模型。对于信心不足的同学来说，分分钟劝退✋✋✋😂
5. paddle平台上的api太多，短时间内不容易弄懂
6. 就七日的实践来看，内容确实有点多，涉及图像识别、物品分类、数据可视化、数据爬取等多个方面，七天学习只能算是开了个头，后面还需要慢慢消化
7. 感谢这段时间群里学习负责人



## 五、未来规划

1. 继续利用paddle平台学习
2. 强化自己的专业能力
3. 仅仅7天的学习只能是一种了解，后面还需要时间来消化这些模型，为自己所用
4. 读论文，复现论文模型

---





最后放上paddle平台链接，加油呀：

**PaddleX官网地址：**

https://www.paddlepaddle.org.cn/paddle/paddlex

![avatar](https://mmbiz.qpic.cn/mmbiz_gif/sKia1FKFiafghJh4BQqez7ZqJtUrD4w0Tic6AWZGtSGNK5GJ6pUPicib5iaBraz0gsNmfSrnC2JPFGQb2o1VPnj1BJ2g/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

![二维码](C:\Users\86177\Desktop\二维码.png)