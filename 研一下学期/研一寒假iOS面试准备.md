# 研一寒假iOS面试
[iOS-Developer-and-Designer-Interview-Questions](https://github.com/9magnets/iOS-Developer-and-Designer-Interview-Questions)
[总结自Interview-Questions](https://github.com/lzyy/iOS-Developer-Interview-Questions)
[总结有参考答案](https://www.jianshu.com/p/d884f3040fda)
[总结](https://segmentfault.com/a/1190000022660286)

## 准备阶段

### 实习经历

百度实习，在百度实习的时候主要复杂凤巢移动端，百度营销App的开发迭代，前期做了一些简单的开发维护工作以及组件维护的工作，还有在实习期间完成了信息流投放的新需求，在这个需求中使用MVVM的思想方式完成，我在这个需求中主要辅助了整体架构的设计，完成了一些控件的封装以及UI界面的编写，在这个需求中我最大的收获是关于需求整体的规划，同时完成了一个小时力度报告的需求，实习期间也修复了一些小问题比如推送，和一些简单的适配问题。

滴滴实习，主要完成了三个事情，首先是关于iOS司机端App的迭代和开发，第二跟进内部项目MockServer项目的开发，项目使用PHP进行开发，主要目的是帮助测试进行mock数据，iOS端使用
NSURLProctor进行流量的转发，第三是和后市场车生活对接，在主站App进行扫描充电柱上的二维码，将相关信息透传给车生活部分。

### 项目经历（见简历）
熟悉简历的内容，将简历说到的点进行细化。

### 基础知识

* 响应链相关内容 [参考](https://www.jianshu.com/p/9179e5d780c8)
* UIview和CALayer之间的关系
    * UIView显示在屏幕上归功于CALayer，通过调用drawRect方法来渲染自身的内容，调节CALayer属性可以调整UIView的外观，UIView继承自UIResponder，CALayer不可以响应用户事件
    * UIView是iOS系统中界面元素的基础，所有的界面元素都继承自它。它内部是由Core Animation来实现的，它真正的绘图部分，是由一个叫CALayer(Core Animation Layer)的类来管理。UIView本身，更像是一个CALayer的管理器，访问它的根绘图和坐标有关的属性，如frame，bounds等，实际上内部都是访问它所在CALayer的相关属性
    * UIView有个layer属性，可以返回它的主CALayer实例，UIView有一个layerClass方法，返回主layer所使用的类，UIView的子类，可以通过重载这个方法，来让UIView使用不同的CALayer来显示   
* frame和bounds区别
    * frame相对于父视图,是父视图坐标系下的位置和大小。bounds相对于自身,是自身坐标系下的位置和大小。
    * frame以父控件的左上角为坐标原点，bounds以自身的左上角为坐标原点

* Load 和 initialize
    * load方法 
    
    > 首先，load方法是一定会在runtime中被调用的，只要类被添加到runtime中了，就会调用load方法，所以我们可以自己实现laod方法来在这个时候执行一些行为。
而且有意思的一点是，load方法不会覆盖。也就是说，如果子类实现了load方法，那么会先调用父类的load方法，然后又去执行子类的load方法。同样的，如果分类实现了load方法，也会先执行主类的load方法，然后又会去执行分类的load方法。所以父类的load会执行很多次，这一点需要注意。而且执行顺序是 类 -> 子类 ->分类。而不同类之间的顺序不一定。

    * initialize
    
    > 与load不同的是，initialize方法不一定会执行，只有当一个类第一次被发送消息的时候会执行，注意是第一次，就是执行一个类的一些方法的时候，也就是说这个方法是懒加载，没有用到这个类就不会调用，可以解决系统资源。还有一点与+load截然相反的就是initialize会覆盖，也就是说如果子类实现了initialize方法就不会执行父类的了，直接执行子类本身的，分类实现了initialize方法就不会执行主类的了，所以initialize方法的执行覆盖顺序是分类 > 子类 > 类 而且只会有一个initialize方法被执行
    
* 属性关键字的区别 [参考](https://www.jianshu.com/p/3020defa685e) 
[参考](https://www.jianshu.com/p/6c8db60c486a)


* KVO&KVC [参考](https://honkersk.github.io/2018/09/12/iOS%E9%9D%A2%E8%AF%95%E9%A2%986-KVO%E5%92%8CKVC/)
[✨ 参考](https://www.jianshu.com/p/47ead92286cd)
    
    * 在runtime动态创建的新类中的setter方法会一次调用
     
     ```
     willChangeValueForKey -> setter(父类方法) -> didChangeValueForKey 
     didChangeValueForKey 内部优惠调用监听器的observeValueForKeyPath监听方法
     ```

     * 手动调用willChangeValueForKey：和 didChangeValueForKey: 就可以手动触发KVO
     
     * KVC 字典转模型 

* atomic 一定是线程安全的么 [参考](https://www.jianshu.com/p/e286d2907bf7) 
  
### 三方库知识

### 算法知识

* 链表翻转
* 求平方根
* 中序前序恢复树

```
public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder == null || preorder.length == 0) {
            return null;
        }
        Map<Integer, Integer> indexMap = new HashMap<Integer, Integer>();
        int length = preorder.length;
        for (int i = 0; i < length; i++) {
            indexMap.put(inorder[i], i);
        }
        TreeNode root = buildTree(preorder, 0, length - 1, inorder, 0, length - 1, indexMap);
        return root;
    }

    public TreeNode buildTree(int[] preorder, int preorderStart, int preorderEnd, int[] inorder, int inorderStart, int inorderEnd, Map<Integer, Integer> indexMap) {
        if (preorderStart > preorderEnd) {
            return null;
        }
        int rootVal = preorder[preorderStart];
        TreeNode root = new TreeNode(rootVal);
        if (preorderStart == preorderEnd) {
            return root;
        } else {
            int rootIndex = indexMap.get(rootVal);
            int leftNodes = rootIndex - inorderStart, rightNodes = inorderEnd - rootIndex;
            TreeNode leftSubtree = buildTree(preorder, preorderStart + 1, preorderStart + leftNodes, inorder, inorderStart, rootIndex - 1, indexMap);
            TreeNode rightSubtree = buildTree(preorder, preorderEnd - rightNodes + 1, preorderEnd, inorder, rootIndex + 1, inorderEnd, indexMap);
            root.left = leftSubtree;
            root.right = rightSubtree;
            return root;
        }
    }
```

* 网络流模板
* 股票买入卖出
* 翻转等价二叉树

```
   public boolean flipEquiv(TreeNode root1, TreeNode root2) {
        if (root1 == root2)
            return true;
        if (root1 == null || root2 == null || root1.val != root2.val)
            return false;

        return (flipEquiv(root1.left, root2.left) && flipEquiv(root1.right, root2.right) ||
                flipEquiv(root1.left, root2.right) && flipEquiv(root1.right, root2.left));
    }
```

### 计算机基础

#### 计算机网络

* http为什么底层是tcp不是udp ?
* tcp为什么要进行三次握手？不是2次，4次？
* http和socket的区别
* TCP和UDP的区别
* http与https [将的挺详细的](https://www.cnblogs.com/cxuanBlog/p/12490862.html)
* Https中的对称加密和非对称加密
  [简介明了](https://www.jianshu.com/p/918d9f517749)
  使用非对称加密传输一个对称密钥K，让服务器和客户端都得知。然后两边都使用这个对称密钥K来加密解密收发数据。因为传输密钥K是用非对称加密方式，很难破解比较安全。而具体传输数据则是用对称加密方式，加快传输速度。两全其美。
  
* TCP三次握手四次挥手及time_wait状态解析
  [参考链接](https://blog.csdn.net/weixin_42250655/article/details/88659118)

#### 操作系统

* 堆和栈的区别 [参考](https://zhuanlan.zhihu.com/p/59195787)
[✨✨参考](https://blog.csdn.net/K346K346/article/details/80849966)

* 进程与线程的区别 [参考链接](https://blog.csdn.net/mxsgoden/article/details/8821936)
[更符合面试要求](https://www.nowcoder.com/questionTerminal/234895a70e0b40e19db7f3fbaabc5fa3)

    进程是运行中的程序，线程是进程的内部的一个执行序列
    进程是资源分配的单元，线程是执行行单元
    进程间切换代价大，线程间切换代价小
    进程拥有资源多，线程拥有资源少
    多个线程共享进程的资源

## 参考面经部分




https://blog.csdn.net/weixin_42250655/article/details/88659118


