# leetcode刷题笔记
## 数组
1.二分查找<br>
2.移除元素<br>
3.有序数组的平方<br>
4.长度最小的子数组<br>
5.螺旋矩阵Ⅱ<br>
6.区间和<br>
7.开发商购买土地<br>
## 链表
1.移除链表元素<br>
2.设计链<br>
3.翻转链表<br>
4.两两交换链表中的节点<br>
5.删除链表的倒数第N个节点<br>
6.链表相交<br>
7.环形链表Ⅱ<br>
## 哈希表
1.有效的字母异位词<br>
2.两个数组的交集<br>
3.快乐数<br>
4.两数之和<br>
题目难度：easy
思路：
两次遍历，找到符合条件的2个数，构建一个2个元素的数组把他们输出即可。
```
int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    for (int i=0;i<numsSize;++i){
        for (int j=i+1;j<numsSize;++j){
            if (nums[i]+nums[j]==target)
        {
            int *result=malloc(sizeof(int)*2);
            result[0]=i,result[1]=j;
            *returnSize=2;
            return result;
        }
        }
    }
    *returnSize=0;
    return NULL;
}
```
5.四数相加Ⅱ<br>
6.赎金信<br>
7.三数之和<br>
8.四数之和<br>
## 字符串
1.反转字符串<br>
2.反转字符串Ⅱ<br>
3.替换数字<br>
4.翻转字符串里的单词<br>
5.右旋转字符串<br>
6.实现strstr()<br>
7.重复的子字符串<br>
## 栈与队列
1.用栈实现队列<br>
2.用队列实现栈<br>
3.有效的括号<br>
4.删除字符串中的所有相邻重复项<br>
5.逆波兰表达式求值<br>
6.滑动窗口最大值<br>
7.前K个高频元素<br>
## 二叉树
1.二叉树的递归遍历<br>
2.二叉树的迭代遍历<br>
3.二叉树的统一迭代法<br>
4.二叉树的层序遍历<br>
5.翻转二叉树<br>
6.对称二叉树<br>
7.二叉树的最大深度<br>
8.二叉树的最小深度<br>
## 回溯算法
1.组合问题<br>
2.组合（优化）<br>
3.组合总和Ⅲ<br>
4.电话号码的字母组合<br>
5.组合总和<br>
6.组合总和Ⅱ<br>
7.分割回文串<br>
8.复原IP地址<br>
9.子集问题<br>
## 贪心算法
1.分发饼干<br>
2.摆动序列<br>
3.最大子序和<br>
4.买卖股票的最佳时机Ⅱ<br>
5.跳跃游戏<br>
## 动态规划
1.斐波那契数<br>
难度：easy
思路：直接用三个变量num1,num2,result，一个存F(n-2),一个存F(n-1),一个存F(n),输出最后一个变量即可。
```
int fib(int n) {
    if(n<2){
        return n;
    }
    int num1=0;
    int num2=0;
    int result=1;
    for(int i=2;i<=n;++i){
        num1=num2;
        num2=result;
        result=num1+num2;
    }
    return result;
}
```
2.爬楼梯<br>
3.使用最小花费爬楼梯<br>
4.不同路径<br>
5.不同路径Ⅱ<br>
## 单调栈
1.每日温度<br>
2.下一个更大元素Ⅰ<br>
3.下一个更大元素Ⅱ<br>
4.接雨水<br>
5.柱形图中最大的矩形<br>
## 图论
1.所有可达路径<br>
2.岛屿数量深搜版<br>
## 额外题目
1.有多少小于当前数字的数字<br>
2.有效的山脉数组<br>
3.独一无二的出现次数<br>
4.移动零<br>
5.旋转数组<br>
6.寻找数组的中心索引<br>