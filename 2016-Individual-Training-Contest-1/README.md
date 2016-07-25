#Round 1

##T1

###Pro

给出一个可进行交换操作的整数序列， 要求在n次操作内完成对序列的排序， 求方案.

###Sol

n只有3000， 因此O(n²)的算法完全可行. 考虑从左到右使序列有序， 则每次找到当前位置对应的值， 再向后查找另一个值的位置并将两者交换即可.

##T2

###Pro

对于一个有向图， 若其中的四个点a、b、c、d满足a->b,b->d,a->c,c->d的关系， 则对其计数， 求一个有向图中共有多少这样的集合.

###Sol

n仍然只有3000. 每组关系中， 起点和终点都是固定的， 故从满足关系的集合中的起点即a点出发， 对每个点进行深度为2的搜索并对终结点被访问次数计数， 表示从a出发有cnt条通路到达d点， 则对答案的贡献为cnt*(cnt-1)/2， 将每个点求和即可.

##T5

###Pro

二分图中， 每个点有相应的权值， 当两点之间权值差不超过1时可进行匹配， 求最大匹配.

###Sol

枚举建图后直接二分图匹配即可.

##T6

###Pro

给出一个数的位数及各位上的数字的和， 求满足条件的最大和最小的数.

###Sol

易证贪心算法的正确性， 即高位可放置大数时， 所得结果一定比放置在低位时大， 反之亦然. 则直接从高位向下贪心即可.

注意：首位不能为0.

##T7

###Pro

一个含n个元素的集合中， 定义其子集的价值为子集中最小元素的值， 求所有奇数个元素的子集的价值和与所有偶数个子集的价值和的差.

###Sol

若一个集合含k个元素， 则有C(n,k)个相同大小的集合， 对原集合排序后， 在子集大小为k时， 每个元素对答案的贡献为a[i] * C(n-i, k-1)，预处理出组合数表后可直接求和.

##T9

###Pro

若一个正整数只由4和7构成， 记该数为幸运数， 若其中4和7出现次数相同， 则记为超级幸运数， 给出一个数n， 求不比n小的最小的超级幸运数.

###Sol

观察发现答案最大只有20位， 而且只由两个数字组成， 因此超级幸运数的数量和不超过2^20， 且由于位数和数量的限制远小于此， 故可以先预处理出所有的超级幸运数， 然后对n二分查找即可.

但手动二分太麻烦， 我们可以直接将这些数放入set中， 每次取lower_bound的值即可.

**此题有坑点**：由于n最大可达10^18，其答案的长度到了二十位数的级别， unsigned long long也是存不下的， 必须进行特判， 否则罚时起飞.

##T10

###Pro

将一条长度为n的钢筋(?)切割成更短的， 要求切割后的部分两两不相等且任意两者加起来不能长于任意一部分， 求最多能分为多少份.

###Sol

由于两者之和不能超过其余部分， 可见长度从小到大排序后应呈斐波那契形式的增长， 那么直接求不大于n的最大斐波那契数即可.  最终分配方案应与斐波那契数列成比例.

若n值极大， 可考虑矩阵快速幂加二分优化， 不过这里n只有long long级别， 可直接递推.