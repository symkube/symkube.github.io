符号运算的对象

repr打印信息

首先是数值对象，要有一个初始化数值，要有基本的对象间加减乘除

`__add__`、`__mul__`魔法函数

还有备用的 `__rmul__`等

r系列的二元运算，`  def __radd__(self, other): # other + self ` 这里面的self和other其实已经交换了

除法基于指数定义为`x^-1`，只搞了scalar power和exp

一个特殊的地方：
```
  def exp(self):
    x = self.data
    out = Value(exp(x), (self, ), 'exp')

    def _backward():
      self.grad += out.data * out.grad
    out._backward = _backward

    return out
```

上游梯度当然是out.grad

而局部梯度是 out.data，因为 e^x 这个函数的导数恰好就是它自己 e^x。而 out.data 正是我们在前向传播中计算并存储下来的 e^x 的值。


---

为了实现微分的图结构（dag），对象中还要储存operation和两个孩子

---

接下来就是比较吓人的，计算图的结构可视化

基于graphviz

整体就是一个单点打印和一个递归搜索

每个点打印operation，一个、两个或多个孩子

对象中可以再加一个变量名的标签

---

一些参数是data，一些参数是param，我们关心的是params的变化如何影响最终结果

对象中还要为每个param记录grad

---

算符并不知道整个计算图的其他部分

---

首先确定了out node 的grad，然后通过拓扑排序向前推

需要注意，一个node可能指向多个其他node，此时要把grad累积起来

---

整体来说是一个二叉树结构，只不过有些更孩子的节点可以合并，每个（二元运算）符号连接了三个部分（三个 node 对象）

最主要的数据就是此处的param和grad，根据grad更新param

---

传引用机制在数据处理上很方便，直接写个函数遍历就行

同时我们总是只需要建立一个需要处理的数据的列表，然后直接处理就够了

---

most common neural net mistakes: 1) you didn't try tooverfit a single batch first. 2) you forgot to toggle train/eval mode for the net. 3) you forgot to .zero_grad() (in pytorch) before .backward(). 4)youpassed softmaxed outputs to a loss that expects rawlogits. ; others? :)

---

zip是惰性求值，在长度不等时到最短的结束