# 目录
<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
<!--te-->

----

# 初级算法

## 求解素数(质数)

有三种方法：

1. 根据定义循环判断该数除以比他小的每个自然数（大于1），如果有能被他整除的就不是质数：
2. 利用定理：如果一个数是合数，那么它的最小质因数肯定小于等于它的平方根。所以判断一个数是否是质数，
只需判断它是否能被小于它开根后的所有数整除。这样做的运算会少很多。
3. 利用定理：如果一个数是合数，那么它的最小质因数肯定小于等于它的平方根。
我们可以发现只要尝试小于等于平方根的所有数即可。列举从 3 到根号x的所有数，
还是有些浪费。比如要判断101是否质数，101的根号取整后是10，需要尝试的数是1到10。
但是可以发现，对9的尝试是多余的。不能被3整除，必然不能被9整除……顺着这个思路走下去，
其实，只要尝试小于根号x的质数即可。而这些质数，恰好前面已经算出来了，已经存在res中了。

```python
import math

class PrimeNumbers(object):

    def __init__(self, start, end):
        self.start = start
        self.end = end
        self.prime = []

    # 方法1(速度最慢)：
    def isPrimerNum1(self, k):
        if k < 2:
            return False
        for i in range(2, k):
            if k % i == 0:
                return False
        return True
    
    # 方法2(速度次快)：
    def isPrimeNum2(self, k):
        if k < 2:
            return False
        for i in range(2, int(math.sqrt(k)+1)):
            if k % i == 0:
                return False
        return True

    # 方法3(速度最快)：
    def isPrimeNum3(self, k):
        if k < 2:
            return False
        for i in self.prime:
            if k % i == 0:
                return False
        self.prime.append(k)
        return True

    def __iter__(self):
        for i in range(self.start, self.end+1):
            if self.isPrimeNum3(i):
                yield(i)


for i in PrimeNumbers(0, 100):
	print(i)
# 结果为： 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 
# 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97
```

## 深度优先和广度优先

```
             a
           /   \
          b     c
         / \   / \
        d   e f   g
           /
          i
```

深度优先通过递归来实现：

```python
def depth_tree(tree_node):
	if tree_node is not None:
		print(tree_node._data)
		if tree_node._left is not None:
			return depth_tree(tree_node._left)
		if tree_node._right is not None;
			return depth_tree(tree_node._right)
```

广度优先通过队列来实现：

```python
def level_queue(root):
	if root is None:
		return
	my_queue - []
	node = root
	my_queue.append(node)
	while my_queue:
		node = my_queue.pop(0)
		print(node.elem)
		if node.lchild is not None:
			my_queue.append(node.lchild)
		if node.rchild is not None:
			my_queue.append(node.rchild)
```
