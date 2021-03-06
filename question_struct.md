## B(B-)树：   
1.根结点至少有两个子女。        
2.每个中间节点都包含k-1个元素和k个孩子，其中 ceil（m/2） ≤ k ≤ m     
3.每一个叶子节点都包含k-1个元素，其中 ceil（m/2） ≤ k ≤ m       
4.所有的叶子结点都位于同一层。      
5.每个节点中的元素从小到大排列，节点当中k-1个元素正好是k个孩子包含的元素的值域划分      
6.每个结点的结构为：（n，A0，K1，A1，K2，A2，…  ，Kn，An）      
    其中，Ki(1≤i≤n)为关键字，且Ki<Ki+1(1≤i≤n-1)。       
Ai(0≤i≤n)为指向子树根结点的指针。且Ai所指子树所有结点中的关键字均小于Ki+1。 
n为结点中关键字的个数，满足ceil(m/2)-1≤n≤m-1。      

ps:ceil（3/2）=2, m(阶)：最大子节点数   

## B+树：       
1.有k个子树的中间节点包含有k个元素（B树中是k-1个元素），每个元素不保存数据，只用来索引，所有数据     
都保存在叶子节点。      

2.所有的叶子结点中包含了全部元素的信息，及指向含这些元素记录的指针，且叶子结点本身依关键字的大小       
自小而大顺序链接。      

3.所有的中间节点元素都同时存在于子节点，在子节点元素中是最大（或最小）元素。        

## 红黑树
- 平衡树是为了解决二叉查找树退化为链表的情况， 红黑树是为了解决平衡树在插入、删除等操作需要频繁调整的情况。



## 二分搜索树（BST）
- 要求：数据必须有可比较性
- 每个节点的值都大于左子树所有节点的值
- 每个节点的值都小于于右子树所有节点的值
- 赠、查、删 时间复杂度是 O（log n）



## 平衡二叉树（AVL树）
- AVL树，是一种平衡(balanced)的二叉搜索树
- 任意一个结点的key，比它的左孩子key大，比它的右孩子key小
- 对于任意一个节点，左子树和右子树高度差不大于 1 
- AVL 是对 BST 的改进，防止二叉树出现链表的情况
- 最差情况下也是 O(log(n))

- 右旋
    - 旋转节点的左孩子变成根节点，此根节点的右孩子为旋转节点
    - 此根节点原本的右孩子变成旋转节点的左孩子

- 左旋
    - 旋转节点的右孩子变成根节点，此根节点的左孩子为旋转节点
    - 此根节点原本的左孩子变成旋转节点的右孩子

- 四种不平衡情况
    - LL： 左子树大于右子树 and 不平衡节点的左孩子的平衡度 >= 0, 右旋
    - RR： 右子树大于左子树 and 不平衡节点的右孩子的平衡度 <= 0，左旋
    - LR： 左子树大于右子树 and 不平衡节点的左孩子的平衡度 < 0，先左旋（不平衡节点的左孩子）变成LL， 后右旋（不平衡节点）
    - RL： 右子树大于左子树 and 不平衡节点的右孩子的平衡度 > 0， 先右旋（不平衡节点的右孩子）变成RR， 后左旋（不平衡节点）


## （trie树）字典树
- 多叉树
- 查询每个条目的时间复杂度与一共有多少条目无关， 与条目（字符串）的长度有关
- 高阶：压缩字典树、三分搜索树


## 红黑树(红黑树保证最长路径不超过最短路径的二倍，因而近似平衡)：    
- 前言：2-3树（2节点、3节点指拥有的子节点数目）
    - 满足二分搜索树的基本性质（值左小右大）
    - 每个节点存放一个或两个值
    - 绝对平衡（从根节点到任意叶子节点经过的节点数目都相同）
    
1. 每个节点颜色不是黑色，就是红色            
2. 根节点是黑色的        
3. 每个叶节点(nil或空节点)是黑色的。     
4. 如果一个节点是红色，那么它的两个子节点就是黑色的（没有连续的红节点）   
5. 对于每个节点，从该节点到其后代叶节点的简单路径上，均包含相同数目的黑色节点     

推论：      
1. 对每个红色节点，子节点只有两种情况：要么都没有，要么都是黑色的。（不然会违反特征四）    

2. 对黑色节点，如果只有一个子节点，那么这个子节点，必定是红色节点。（不然会违反特征五）       

3. 假设从根节点到叶子节点中，黑色节点的个数是h, 那么树的高度H范围 h<= H <= 2h（特征四五决定）。      

- 左旋：以某个结点作为支点(旋转结点)，其右子结点变为旋转结点的父结点，    
    右子结点的左子结点变为旋转结点的右子结点，左子结点保持不变  
![左旋](../pictures/left_rotate.jpg)

- 右旋：以某个结点作为支点(旋转结点)，其左子结点变为旋转结点的父结点，    
    左子结点的右子结点变为旋转结点的左子结点，右子结点保持不变  
![左旋](../pictures/right_rotate.jpg)   

## 快排优化： 
- 当待排序序列的长度分割到一定大小后，使用插入排序 
- 聚集元素
    - 在一次分割结束后，将与本次基准相等的元素聚集在一起，再分割时，不再对聚集过的元素进行分割。具体过程有两步：
        - 在划分过程中将与基准值相等的元素放入数组两端
        - 划分结束后，再将两端的元素移到基准值周围。



## 分治算法：
- 含义：将一个难以直接解决的大问题，分割成一些规模较小的相同问题。（二分搜索、快排）
- 将原问题分解为若干个规模较小，相互独立，与原问题形式相同的子问题
- 若子问题规模较小而容易被解决则直接解，否则递归地解各个子问题
- 将各个子问题的解合并为原问题的解