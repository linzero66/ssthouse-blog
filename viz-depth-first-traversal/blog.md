# 可视化讲解 深度优先遍历(DFT)

深度优先遍历, 刷过题的朋友应该都很熟悉了,难是不难,但是理解起来还是要费一些功夫的.
深度优先遍历的实现方法有递归和非递归两种, 这里我们用可视化的角度,讲解前一种: 递归的深度优先遍历

为什么要以可视化的方式来讲解呢? 因为人是视觉的动物, 如果和你说 `二叉树` 或 `栈` , 相信大家脑中出现的都是下面的图形:

![binary tree](https://raw.githubusercontent.com/ssthouse/d3-blog/master/viz-depth-first-traversal/img/binary-tree.png)

![stack](https://raw.githubusercontent.com/ssthouse/d3-blog/master/viz-depth-first-traversal/img/stack.jpg)

而不是下面的代码:

```javascript
// binary tree
class Node {
  constructor(value, leftChild, rightChild) {
    this.value = value
    this.leftChild = leftChild
    this.rightChild = rightChild
  }
}

// stack
const stack = new Array()
stack.push(1)
var topItem = stack.pop()
```

所以说, 人是视觉动物, 以图形可视化的方式来讲解问题往往能讲解的更清楚, 这也就是我写本文的缘由.

## 效果展示

为了可视化的讲解 `深度优先遍历算法`, 笔者写了一个简单的网页, 实现的功能有:

- 用户可编辑进行深度遍历的二叉树
- 网页上给出了 JavaScript 版本的实现
- 点击 `Start DFT` 按钮, 用户将看到算法中用到的 **二叉树** 和 **栈** 都将动态 的展示再页面中,可以直观的看到代码运行过程中,数据的变化

页面目前还在继续优化中， 让我们看看目前的效果：

![stack](https://raw.githubusercontent.com/ssthouse/d3-blog/master/viz-depth-first-traversal/img/demo.gif)



可以看到，网页模拟了深度搜索时二叉树和栈的动态变化过程：

- 二叉树中当前被遍历到的节点会变成红色
- 栈中压入 （push）的节点为灰色
- 栈中弹出 （pop) 的节点会变为红色， 然后消失

其中页面左上角为初始遍历的二叉树数据， 用户可以自行修改二叉树数据后再次启动可视化深度优先遍历过程。

页面左下角为深度优先遍历的javascript实现版本，作为参考。

## 深度搜索简介

可视化分析之前，让我们简单看看实现深度优先搜索的代码：

```javascript
export class Dft {
  constructor(rootNode, stepCallback) {
    this.rootNode = rootNode
    this.stepCallback = stepCallback
  }

  start() {
    if (!this.rootNode || !this.stepCallback) {
      return
    }
    const stack = [this.rootNode]
    while (stack.length !== 0) {
      const curNode = stack.pop()
      console.log(`current node: ${curNode.value}`)
      curNode.childrenNodes.forEach(element => {
        stack.push(element)
      })
    }
  }
}

export class Node {
  constructor(value, childrenNodes = []) {
    this.value = value
    this.childrenNodes = childrenNodes
  }
}
```

代码不长，让我们一步步看。



首先我们创建了一个栈 `const stack = [this.rootNode]` , 并将根节点放入栈中.

接下来是一个while语句, 跳出循环的条件是 栈为空, 也就是代表我们遍历完了整棵树.



在循环中, 我们先将栈顶的节点弹出, 并打印出来, 表示我们已经遍历过了该节点. 然后将该节点的所有子节点压入栈中, 这就保障了我们下一个遍历到的点就是该节点的子节点. 重复该循环, 最后我们就可以看到, 二叉树的每个节点都按照深度搜索的顺序被打印了出来:

```
current node: 1
current node: 4
current node: 7
current node: 6
current node: 2
current node: 5
current node: 3
```

如果是对栈的使用比较熟悉的同学, 可能看到这里就已经明白原理了. 但是, 如果是对栈使用不是很熟悉的同学, 估计对代码的执行过程还是没有一个直观的认识, 那么让我们以更直观的方式看看这段代码是怎么运行的.

## 可视化讲解

![step1](https://raw.githubusercontent.com/ssthouse/d3-blog/master/viz-depth-first-traversal/img/step1.png)



## 代码讲解