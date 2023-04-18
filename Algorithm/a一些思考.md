#### 对于变量的理解

- 变量应当看作指针，保存所代表数据的地址，当变量被修改的时候其实是其保存的地址被修改，原地址还保存着原来的数据。比如对于一个TreeNode root，让另一个TreeNode right=root.right，修改right=null，root.right的值不会有变化。