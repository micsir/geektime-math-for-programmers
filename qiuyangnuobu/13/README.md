## 树的广度优先搜索（上）：人际关系的六度理论是真的吗？

### 无向图

在数学里，为了表示这种好友关系，我们通常使用图中的结点来表示一个人，而用图中的边来表示人和人之间的相识关系，那么社交网络就可以用图论来表示。而“相识关系”又可以分为单向和双向。

单向表示，两个人 a 和 b，a 认识 b，但是 b 不认识 a。如果是单向关系，我们就需要使用有向边来区分是 a 认识 b，还是 b 认识 a,如果是双向关系，双方相互认识，因此直接用无向边就够了。

### 深度优先搜索面临的问题

深度优先搜索不仅可以用在树里，还可以应用在图里
面临的问题是图中可能存在回路，这会增加通路的长度，这是我们在计算几度好友时所不希望的
所以在使用深度优选搜索的时候，一旦遇到产生回路的边，我们需要将它过滤。具体的操作是，判断新访问的点是不是已经在当前通路中出现过，如果出现过就不再访问。

### 六度理论
你的社会关系会随着关系的度数增加，而呈指数级的膨胀。这意味着，在深度搜索的时候，每增加一度关系，就会新增大量的好友
二度好友就是 100^2 三度好友就是 100^3 ... 五度好友就有 100 亿人了 已经超过了地球目前的总人口
例如，你的一度好友可能也出现在你的三度好友中，那这也不可能改变结果的数量级。所以目前来看，地球上任何两个人之间的社会关系不会超过六度。

### 广度优先搜索（Breadth First Search）也叫宽度优先搜索

更高效的做法是，我们只需要先找到所有二度的好友，如果二度好友不够了，再去找三度或者四度的好友。这种好友搜索的模式，其实就是广度优先搜索。

是指从图中的某个结点出发，沿着和这个点相连的边向前走，去寻找和这个点距离为 1 的所有其他点。只有当和起始点距离为 1 的所有点都被搜索完毕，才开始搜索和起始点距离为 2 的点。当所有和起始点距离为 2 的点都被搜索完了，才开始搜索和起始点距离为 3 的点，如此类推。

用结点边上的数字表示该结点在广度优先搜索中被访问的顺序。广度优先搜索其实就是横向搜索一颗树啊。

广度优先和深度优先搜索的顺序是不一样的，它们也有两个共同点。

- 在前进的过程中，我们不希望走重复的结点和边，所以会对已经被访问过的点做记号，而在之后的前进过程中，就只访问那些还没有被标记的点。这一点上，广度优先和深度优先是一致的。有所不同的是，在广度优先中，如果发现和某个结点直接相连的点都已经被访问过，那么下一步就会看和这个点的兄弟结点直接相连的那些点，从中看看是不是有新的点可以访问。

- 广度优先搜索也可以让我们访问所有和起始点相通的点，因此也被称为广度优先遍历。如果一个图包含多个互不连通的子图，那么从起始点开始的广度优先搜索只能涵盖其中一个子图。这时，我们就需要换一个还没有被访问过的起始点，继续深度优先遍历另一个子图。深度优先搜索可以使用同样的方式来遍历有多个连通子图的图，这也回答了上一讲的思考题。

### 实现社交好友推荐

深度优先是利用递归的嵌套调用、或者是栈的数据结构来实现的。然而，广度优先的访问顺序是不一样的，我们需要优先考虑和某个给定结点距离为 1 的所有其他结点。
等距离为 1 的结点访问完，才会考虑距离为 2 的结点。
等距离为 2 的结点访问完，才会考虑距离为 3 的结点等等。
在这种情况下，我们无法不断地根据结点的边走下去，而是要先遍历所有距离为 1 的点。

如何在记录所有已被发现的结点情况下，优先访问距离更短的点呢
和起始点更近的结点，会先更早地被发现。也就是说，越早被访问到的结点，越早地处理它 类似于平时排队的情形。

### 先进先出（First In First Out）

早到的人可以优先接受服务，而晚到的人需要等前面的人都离开，才能轮到。所以这里我们需要用到队列这种先进先出（First In First Out）的数据结构。

### 小结

在遍历树或者图的时候，如果使用深度优先的策略，被发现的结点数量可能呈指数级增长。如果我们更关心的是最近的相连结点，比如社交关系中的二度好友，那么这种情况下，广度优先策略更高效。也正是由于这种特性，我们不能再使用递归编程或者栈的数据结构来实现广度优先，而是需要用到具有先进先出特点的队列。