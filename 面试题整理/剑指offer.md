1. 将一个string转化为整数
int convert(const * str)
考虑特殊的输入：空指针，+/-号，数字溢出，不合法字符

2. 求链表倒数第k个节点
快慢指针
快指针先走k步，然后快慢指针一起走，直到快指针到达尾部。
特殊考虑：k是否合法(k是否大于链表的长度，k<=0时)
拓展：
求链表中间结点：快慢指针，一个走一步一个走两步
判断链表是否成环：快指针能否追上慢指针
3. 写一个赋值函数
```c++
CMyString& CMyString::operator=(const CMyString &str){
    if(this != &str){
        CMyString tmp(str);
        char * pTemp = strTemp.m_pData;
        strTemp.m_pData = m_pData;
        m_pData = pTemp;
    }
    return * this;
}
```


4. 杨氏矩阵
1 2 8 9
2 4 9 12
4 7 10 13
6 8 11 15
从右上角或者左下角出发查找目标值。

5. 替换空格
"we are happy"转为“we%20are%20happy”
首先计算替换空格后的长度(len+空格数*2)
然后从后往前进行复制，遇到空格就替换为“%20”
记住：结尾有“\0”

6. 链表
```c++
void AddToTail(ListNode** pHead, int val){
    ListNode* node = new ListNode();
    node->m_nValue = val;
    node->m_pNext = NULL;
    if(*pHead==NULL){
        * pHead = node;
    }else{
        ListNode* p = * pHead;
        while(p->next!=NULL){
            p = p->next;
        }
        p->next = node;
    }
}
void RemoveNode(ListNode** pHead, int val){
    if(**pHead ==NULL || *pHead ==NULL){
        return ;
    }

    ListNode* toBeDeleted = NULL;
    if((* pHead)->m_nValue==val){
        toBeDeleted = (* pHead);
        (* pHead) = (* pHead)->next;
    }else{
        ListNode* p = * pHead;
        while(p->next !=NULL && p->next->m_nValue!=val){
            p = p->next;
        }
        if(p->next!=NULL&&p->next->m_nValue==val){
            toBeDeleted = p->next;
            p->next = p->next->next;
        }
    }
    if(toBeDeleted!=NULL){
        delete toBeDeleted;
        toBeDeleted = NULL;
    }//else的情况就是没找到该节点
}
```

7. 从尾到头打印链表
能否改变链表的结构——能：三个指针进行链表翻转，再输出；不能：放到stack里面再输出或者用递归的方法(可能会有栈溢出)

8. 重建二叉树
已知前序(根左右)和中序(左根右)，重构一个二叉树

9. 用两个栈实现一个队列
push的话先放入s1，然后要pop的时候先看s2有没有值，如果没有值，就将s1的都放到s2里面，然后把s2的栈顶输出；否则直接将s2的栈顶输出

两个队列实现一个栈
push
如果两个que都为空，将数据放入到任意一个que中。
如果其中一个非空，就将数据放到这个que中。
pop
将非空的que中前count-1个移到另一个que，然后输出最后一个值

10. 快排
```c++
void quicksort(vector<int>nums, int start, int end){
    if(start>=end){
        return;
    }
    int first = start;
    int last = end;
    int key = nums[first];
    while(first<last){
        while(first<last&&nums[first]<=key){
            first++;
        }
        nums[last] =  nums[first];
        while(first<last&&nums[last]>key){
            last--;
        }
    }
    nums[first] = key;
    quicksort(nums, start, first-1);
    quicksort(nums, first+1, end);
}
```

| 排序算法| 最好时间复杂度| 最坏时间复杂度|
|---|---|---|
|快排|O(nlogn)|O(n^2)|
|堆排|O(nlogn)|O(nlogn)|
|归并|O(nlogn)|O(nlogn)|
|冒泡|O(n^2)|O(n)|
|插入|O(n^2)|O(n)|

二分查找 最好的时间复杂度是O(1)，最坏的时间复杂度是O(log2N)

11. 根据年龄来排序
排序问题一般要问清楚数据规模，数据类型，是否已经排序，能否使用辅助内存
这里的按照年龄来排序，排序的数组是在一个较小的范围，并且可以使用辅助内存，我们直接对年龄进行排序即可（哈希表），空间复杂度是O(n)
如果想要减少内存(其实这里没什么必要)，可以尝试用位图法

12. 旋转数组的最小数字
{3,4,5,1,2}求其中最小的值
最容易想到的方法当然是遍历一遍记录最小值，时间复杂度是O(n)
可以看到其实最小的那个数将这个数组分成了两个有序的数组。{3,4,5}和{1,2}
这样我们可以尝试用二分法，时间复杂度是O(logn)
```c++
int minval(vector<int>nums, int p1, int p2){
	if(p1>=p2){
		return -1;
	}
	while(p2-p1>1){
		int mid = (p1+p2)/2;
		if(nums[p1]<=nums[mid]){
			p1 = mid;
		}else if(nums[p2]>=nums[mid]){
			p2 = mid;
		}
	}
	if(p2-p1==1){
		return nums[p2];
	}else{
		return -1;
	}
}
```
考虑特殊情况，如果旋转数组是{1,0,1,1,1}
当nums[p1] == nums[mid] == nums[p2]的时候我们直接用遍历的方式找到最小值。不然会陷入死循环。

13. 递归和循环
递归：将一个问题分解成一个或者多个小问题。函数调用自身
问题：栈溢出
优点：简洁
缺点：时间(往栈里压入数据弹出数据)空间(内存栈需要保存参数、返回地址和临时变量)的消耗、计算重复影响性能，调用栈溢出

14. 斐波那契数组
```c++
//版本1：递归
int fib(int n){
    if(n<=0){
        return 0;
    }
    if(n==1){
        return 1;
    }
    return fib(n-1)+fib(n-2);
}
//版本2:循环
int fib2(int n){
    if(n<=0){
    	return 0;
	}
    if(n==1){
        return 1;
    }
    if(n==2){
        return 2;
    }
    int a = 1;
    int b = 2;
    for(int i=2;i<n;i++){
        int tmp = a+b;
        a = b;
        b = tmp;
    }
    return b;
}
```
15. 斐波那契的拓展
青蛙跳台阶：一次可以跳1级，一次可以跳2级------fib可做
青蛙跳台阶进阶版：可以跳1、2、3...n级-----推导递推公式，等比数列
矩形覆盖：1*2和2*1的矩形覆盖一个大矩形------fib可做

16. 位运算
正整数 左移右移是要补零
负数 左移右移要补1

- 如何表示一个负数
原码 0010 转二进制
反码 1101 取反
补码 1110 加一

17. 判断二进制里面有多少个1
```c++
//解法1：不会引起死循环
int countNumberof1(int n){
    int flag = 1;
    int count = 0;
    while(flag){
        if(n&flag==1){
            count++;
        }
        flag = flag<<1;
    }
    return count;
}
//解法2:把一个整数减去1，再与原整数做与运算，会把该整数最右边的1变成0
int countNumberof1(int n){
    int count = 0;
    while(n){
        ++count;
        n = (n-1) & n;
    }
    return count;
}
```
拓展1：判断一个无符号的整数是不是2的n次方。(num-1)&num看是否为0
拓展2：两个整数m和n，计算需要改变m的二进制中多少位才能得到n。统计(m^n)结果中1的位数

18. 保证程序的完整性
- 一般我们要测试自己写的函数的时候，从三个方面入手
    - 功能测试: 正常值 随机值 特殊值(有代表性的)
    - 边界测试: 临界值
    - 错误测试：错误输入参数，如何处理
    - 异常测试：异常值
- 处理异常的方式
    - 特殊的返回值
    - 全局变量
    - 异常捕获，try模块和catch模块

19. 数值的整数次方

```c++
double helper(double base, int exponent){
    if(exponent==0){
        return 1;
    }
    int mid = exponent/2;
    double res = helper(base, exponent>>1);
    if(exponent & 0x1==0){
        return res*res;
    }else{
        return res*res*base;
    }
}
bool invalidInput = false;
double Power(double base, int exponent){
    int flag = 1;
    if(exponent==0){
        return 1;
    }
    if(exponent<0){
        if(equal(base, 0.0)){
            invalidInput=true;
            return 0;
        }
        flag = -1;
    }   
    double val = helper(base, flag*exponent);
    if(flag==-1){
        return 1/val;
    }
    return val;
}
bool equal(double a, double b){
    if(abs(a-b)<=0.000001){
        return true;
    }else{
        return false;
    }
}
```
用位运算为替换
%2 可以替换成 &0x1
/2 可以替换成 >> 1

19. 打印1到最大的n位数
最简单的想法当然是for循环，但是有问题。考虑n的值，可能有大数问题，变量值可能会溢出
考虑用数组或者字符串来储存n位数
```c++
bool increment(int *num, int length){
	int step = 0;
	for(int i=length-1;i>=0;i--){
		int sum = num[i]+step;
		if(i==length-1){
			sum++;
		}
		if(sum>=10){
			if(i==0){
				return false;
			}else{
				sum = sum-10;
				num[i] = sum;
				step = 1;
			}
		}else{
			num[i] = sum;
			return true;
		}
	}
}
void print(int *num, int n){
	int i = 0;
	for(i=0;i<n;i++){
		if(num[i]!=0){
			break;
		}
	}
	for(;i<n;i++){
		cout<<num[i];
	}
	cout<<endl;
}
void func(int n){
	if(n<=0){
		return;
	}
	int * num = new int [n+1];
	for(int i=0;i<n;i++){
		num[i] = 0;
	}

	while(increment(num, n)){
		print(num,n);
	}
	delete []num;
}
```

20. 在O(1)时间里删除链表结点
void deletenode(ListNode** pListHead, ListNode* pToBeDeleted);
先找到pToBeDeleted这个节点，然后把他下一个节点的内容复制到要删除的节点上覆盖原来的内容，然后删掉下一个节点
当这个要删除的节点是尾节点时，我们要重新遍历链表，找到它的前序节点，并把这个节点的next置为空，完成删除操作。
只有一个节点的时候，刚好又要删除头节点，我们删除节点后，要将头指针置为NULL

平均时间复杂度：[(n-1)* O(1)+O(n)]/n = O(1)
如果要删除的节点不在链表里面呢？顺序查找，判断一次。O(n)

21. 调整数组顺序使得奇数在偶数前面
双指针

22. 翻转链表
方法1：三个指针 prev current Next
```c++
ListNode* Reverse(ListNode* pHead){
    if(pHead==NULL||pHead->next== NULL){
        return pHead;
    }
    ListNode* p = pHead;
    ListNode * prev ==NULL;
    ListNode* current = pHead;
    ListNode * next = NULL;
    while(current->next){
        next = current->next;
        if(next==NULL){
            p = current;
        }
        current->next = prev;
        prev = current;
        current = next;
    }
    return p;

}
```
方法2：用链表

23. 合并两个排序的链表
```c++
ListNode * merge(ListNode* pHead1, ListNode* pHead2){
    if(pHead1==NULL){
        return pHead2;
    }
    if(pHead2==NULL){
        return pHead1;
    }
    ListNode * mergeHead == NULL;
    if(* pHead1<* pHead2){
        mergeHead = pHead1;
        mergeHead->next = merge(pHead1->next, pHead2);
    }else{
        mergeHead = pHead2;
        mergeHead->next = merge(pHead1, pHead2->next);
    }
    return mergeHead;
}
```

24. 看树A是否树B的子结构
```c++
bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
{
    if(pRoot1==NULL||pRoot2==NULL){
        return false;
    }
    return helper(pRoot1,pRoot2)||HasSubtree(pRoot1->left, pRoot2)||HasSubtree(pRoot1->right, pRoot2);
}
bool helper(TreeNode* pRoot1, TreeNode* pRoot2){
    if(pRoot2==NULL){
        return true;
    }
    if(pRoot2!=NULL&&pRoot1==NULL){
        return false;
    }
    if(pRoot1->val==pRoot2->val){
        return helper(pRoot1->left, pRoot2->left)&&helper(pRoot1->right, pRoot2->right);
    }else{
        return false;
    }
}
```

25. 二叉树的镜像
递归实现：
先将左右节点进行交换
然后再对左右子树做同样的mirror交换

26. 顺时针打印一个矩阵
用循环来做
start_x start_y
end_x end_y

27. 包含min函数的栈
用两个来实现。栈1正常存入数据，栈2的栈顶始终保持当前的最小值。
栈1:3,4,5,6,1,2
栈2:3,3,3,3,1,1

28. 栈的压入和弹出
判断一个序列是不是栈的弹出序列
比如说入栈序列为{1,2,3,4,5}，那么出栈序列不可能是{4,3,5,1,2}
辅助栈——将{1,2,3,4,5}依次入栈，每次插入时与出栈序列的栈顶比较，如果相同就pop出来。否则继续加入新的数字到辅助栈。当辅助栈入栈完成，就将辅助栈的所有元素pop出来与出栈序列进行对比。如果不一致就表明这个出战序列是错的。

29. 从上往下打印二叉树
用queue
```c++
vector<vector<int>> levelVisit(BinaryTree* root){
    vector<vector<int> result;
    if(root==NULL){
        return result;
    }

    queue<BinaryTree*> que;
    que.push(root);
    while(!que.empty()){
        int size = que.size();
        vector<int>temp;
        for(int i=0;i<size;i++){
            BinaryTree* tmp = que.front();
            temp.push_back(tmp->val);
            que.pop();
            if(tmp->left){
                que.push(tmp->left);
            }
            if(tmp->right){
                que.push(tmp->right);
            }
        }
        result.push_back(temp);
    }
    return result;
}
```
30. 判断一个数组是否二叉树的后序遍历序列
根节点会把数组分成两部分，一部分比根节点小，另一个部分比根节点大。然后再递归判断这两部分。
```c++
bool verifySequenceOfBST(vector<int> seq, int length)
```

31. 二叉树和为某一值的路径
前序遍历
栈调用

32. 复杂链表的复制
- 每个节点复制一个
- 复制每个节点的指向
- 拆分两个链表 返回目标链表

33. 二叉搜索树和双向链表
从根节点划分，根节点的左边指向左子树的最右边的节点；根节点的右边指向右子树的最左边的节点。我们递归调用这个函数
最终得到一个双向链表，找到他的头部并返回

34. 字符串排列
用backtracking？
把字符分成两个部分，第一个部分是字符串的第一个字符，第二部分是剩下的全部字符，然后求后面部分的全排列。
拿第一个字符与后面的字符逐个交换。

35. 数组中找到出现次数超过一半的数字
- 快排O(n) 找到一个数，左边放比他小的数，右边放比他大的数，看他的下标，如果是n/2,即为所求，如果大于n/2，就在左边找；否则在右边找
遍历一遍数组，看他是否出现次数超过数组大小的一半。
- 保存一个数以及它出现的次数，用来抵消并且计算

36. 最小的k个数

37. 连续数组的最大和
dp[i] = max(num[i], dp[i-1]+num[i])
找到dp数组中的最大值

38. 从1到n整数中1出现的次数

39. 把数组排成最小的数
大数问题
cmp比较 mn与nm比较
传入sort函数中
直接输出 不储存到变量中

40. 丑数
能被2,3 5整除的数
自己构造一个数组，时间换空间

41. 第一个只出现一次的字符
hash表吧

42. 数组中的逆序对
参考归并排序
在合并的时候进行处理。两个数组进行比较，三指针。

43. 两个链表的公共节点
先统计两个链表长度的差值
快慢指针，
快的先走step步，然后一起走，直到相遇

44. 数字在排序数组中出现的次数
排序数组 - 立刻联想到二分查找
这里我们找这个数字在序列中出现的第一个位置，再找它在这个序列中的最后一个位置，然后相减+1即为所求。
`GetFirstK`比较num[mid]与target的值。类比可以写出`GetLastK`
```
int GetFirstK(vector<int>nums, int start, int last, int target){
    mid = (start+end)>>1;
    if(nums[mid]==target){
        if(mid-1>=0&&nums[mid-1]==target){
            last = mid-1;
        }else{
            return mid;
        }
    }else if(nums[mid]>target){
        start = mid+1;
    }else{
        last = mid-1;
    }
    GetFirstK(nums, start, last, target);

}
```
