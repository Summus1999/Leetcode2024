# leetcode刷题笔记
## 数组
1.二分查找<br>
题目难度：easy
思路：
类似武侯猜数，使用二分法，每次都选中间的，然后再调整直到寻到符合条件的数。
```
int search(int* nums, int numsSize, int target) {
    int left = 0;
    int right = numsSize - 1;
    while (left<=right) {
        int middle = left + (right - left) / 2;
        if (nums[middle] > target) {
            right = middle - 1;
        }
        else if (nums[middle] < target) {
            left = middle + 1;
        }
        else {
            return middle;
        }
    }
    return -1;
}
```
2.移除元素<br>
3.有序数组的平方<br>
4.长度最小的子数组<br>
5.螺旋矩阵Ⅱ<br>
6.区间和<br>
7.开发商购买土地<br>
8.找出数组游戏的赢家
题目难度：easy
思路：
找到数组游戏的赢家，也就是设计一个计数器变量count，一个暂时赢家，遍历然后找到符合条件的赢家输出即可。
```
//注意题目中是不同整数，条件判断中没有等号
int getWinner(int* arr, int arrSize, int k) {
    int Maximum = arr[0];
    int count = 0;
    for (int i = 0;i < arrSize;i++) {
        if (count == k) break;
        if (Maximum < arr[i]) {
            Maximum = arr[i];
            count = 1;
        }
        else if (Maximum > arr[i]) {
            count++;
        }
    }
    return Maximum;
}
```
9.一维数组的动态和
题目难度：easy
思路：
确定长度，然后遍历，根据公式，遍历需要从下标1开始，最后输出结果即可。
```
int* runningSum(int* nums, int numsSize, int* returnSize) {
    *returnSize = numsSize;
    for (int i = 1;i < numsSize;i++) {
        nums[i] = nums[i - 1] + nums[i];
    }
    return nums;
}
```
10.移动零
题目难度：easy
思路：
双指针法，如果一个数左指针和右指针指向的值有一个为0，即进行交换，交换为了减小代码量使用函数实现，调用子函数swap实现即可。
```
void swap(int* a,int* b) {
    int t = *a;
    *a = *b;
    *b = t;
}
void moveZeroes(int* nums, int numsSize) {
    int left = 0;
    int right = 0;
    while (right < numsSize) {
        if (nums[right]) {
            swap(nums + left, nums + right);
            left++;
        }
        right++;
    }
}
```
11.分割数组
题目难度：easy
思路：
使用哈希表，如果一个数组内有一个元素出现2次以上则不可分割，反之均可分割。
```
//3046分割数组
bool isPossibleToSplit(int *nums, int numsSize)
{
    int count[101] = {0};
    for (int i = 0; i < numsSize; i++)
    {
        if (++count[nums[i]] > 2)
        {
            return false;
        }
    }
    return true;
}
```
12.满足目标工作时长的员工数目
题目难度：easy
思路：
遍历，满足条件则人数+1即可。
```
//2798满足目标工作时长的员工数目
int numberOfEmployeesWhoMetTarget(int *hours, int hoursSize, int target)
{
    int result = 0;
    for (int i = 0; i < hoursSize; i++)
    {
        if (hours[i] >= target)
        {
            result++;
        }
    }
    return result;
}
```
13.判断是否可以赢得数字游戏
题目难度：easy
思路：
先找到总数，然后统计一位数的和和二位数的和，只有有一个超过一半则返回true
```
//3232判断是否可以赢得数字游戏
bool canAliceWin(int *nums, int numsSize)
{
    int totalValue = 0;
    int num1 = 0;
    int num2 = 0;
    // 统计总数和
    for (int i = 0; i < numsSize; i++)
    {
        totalValue = totalValue + nums[i];
    }
    // 统计1位数的和
    for (int i = 0; i < numsSize; i++)
    {
        if ((nums[i] >= 1) && (nums[i] < 10))
        {
            num1 = num1 + nums[i];
        }
    }
    // 统计2位数的和
    for (int i = 0; i < numsSize; i++)
    {
        if ((nums[i] >= 10) && (nums[i] < 100))
        {
            num2 = num2 + nums[i];
        }
    }
    if ((num1 > totalValue / 2) || (num2 > totalValue / 2))
    {
        return true;
    }
    else
    {
        return false;
    }
}
```
14.买卖股票的最佳时机
题目难度：easy
思路：
追求最大利润，买入价格必须是最低点，售出价格必须是最高点，用一个变量保存最低价格，一个变量保存最高价格，相减即可。<br>
代码：
```
//121买卖股票的最佳时机
#define MAX(a, b) ((a) > (b) ? (a) : (b))
#define MIN(a, b) ((a) < (b) ? (a) : (b))
int maxProfit(int *prices, int pricesSize)
{
    int result = 0;
    int min_price = prices[0];
    for (int i = 0; i < pricesSize; i++)
    {
        int temp = prices[i];
        result = MAX(result, temp - min_price);
        min_price = MIN(min_price, temp);
    }
    return result;
}
```
15.多数元素<br>
题目难度：easy<br>
思路：
先排序然后分类讨论，取中间的数即可。<br>
代码：
```
//169多数元素
int cmp(const void *a, const void *b)
{
    return *(int *)a - *(int *)b;
}
int majorityElement(int *nums, int numsSize)
{
    // 排序，然后直接选中间的一个，分奇数偶数讨论
    qsort(nums, numsSize, sizeof(int), cmp);
    int result = 0;
    if (numsSize % 2 == 0)
    {
        result = numsSize / 2;
        return nums[result];
    }
    else
    {
        result = (numsSize - 1) / 2;
        return nums[result];
    }
}

```
16.删除有效数组中的重复项
题目难度：easy
思路：<br>
双指针，使用快慢指针，如果快指针找到重复项则把这个重复项去掉。<br>
代码：
```
//26删除有序数组中的重复项
int removeDuplicates(int *nums, int numsSize)
{
    if (numsSize <= 0)
    {
        return 0;
    }
    int slow = 1;
    int fast = 1;
    while (fast < numsSize)
    {
        if (nums[fast] != nums[fast - 1])
        {
            nums[slow] = nums[fast];
            ++slow;
        }
        ++fast;
    }
    return slow;
}
```
17.最小数字游戏<br>
题目难度：easy<br>
思路：<br>
先排序，2个为一组，小的数字放后面一个，大数字放前面即可。<br>
代码：
```
//2974最小数字游戏
int cmp(const void *a, const void *b)
{
    return *(int *)a - *(int *)b;
}
int *numberGame(int *nums, int numsSize, int *returnSize)
{
    qsort(nums, numsSize, sizeof(int), cmp);
    *returnSize = numsSize;
    for (int i = 0; i < numsSize; i = i + 2)
    {
        int temp = nums[i];
        nums[i] = nums[i + 1];
        nums[i + 1] = temp;
    }
    return nums;
}
```
18.合并两个有序数组
题目难度：easy
思路：
先合并后排序即可。
代码：
```
//88合并两个有序数组
int cmp(const void *a, const void *b)
{
    return *(int *)a - *(int *)b;
}
void merge(int* nums1, int nums1Size, int m, int* nums2, int nums2Size, int n) {
    for(int i=0;i!=n;++i){
        nums1[m+i]=nums2[i];
    }
    qsort(nums1, nums1Size, sizeof(int), cmp);
}
```
19.数组中两元素的最大乘积
题目难度：easy
思路：
先排序然后直接找2个最大的数算出来即可。
代码：
```
//1464数组中两元素的最大乘积
int cmp(const void *a, const void *b)
{
    return *(int *)a - *(int *)b;
}
int maxProduct(int *nums, int numsSize)
{
    qsort(nums, numsSize, sizeof(int), cmp);
    return (nums[numsSize - 2] - 1) * (nums[numsSize - 1] - 1);
}
```
20.丢失的数字
题目难度：easy
思路：
直接算预期的总和和实际的总和，差值就是丢失的数字。
代码：
```
//268丢失的数字
int cmp(const void *a, const void *b)
{
    return *(int *)a - *(int *)b;
}
int missingNumber(int *nums, int numsSize)
{
    qsort(nums, numsSize, sizeof(int), cmp);
    int expectCount = numsSize * (numsSize + 1) / 2;
    int actualCount = 0;
    for (int i = 0; i < numsSize; i++)
    {
        actualCount = actualCount + nums[i];
    }
    return expectCount - actualCount;
}
```
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
题目难度：easy
思路：
找到符合要求的字符串，将首尾换成符合要求的即可。
```
void swap(char* a, char* b) {
    char t = *a;
    *a = *b;
    *b = t;
}
void reverseString(char* s, int sSize) {
    for (int left = 0, right = sSize - 1; left < right; left++, right--) {
        swap(s + left, s + right);
    }
}
```
2.反转字符串Ⅱ<br>
3.替换数字<br>
4.翻转字符串里的单词<br>
5.右旋转字符串<br>
6.实现strstr()<br>
7.重复的子字符串<br>
8.字符串中的单词数<br>
题目难度：easy<br>
思路：<br>
找到单词计数加1的条件即可，前一个为空后一个为空是一个单词结束的标志，前一个非空后一个遇到结束符\0是句子结束的标志，单词数也要+1。<br>
代码：
```
int countSegments(char* s) {
    int length = strlen(s);
    int count = 0;
    for (int i = 0;i < length;i++) {
        if ((s[i] != ' ' && s[i + 1] == ' ') || (s[i] != ' ' && s[i + 1] == '\0')) {
            count++;
        }
    }
    return count;
}
```
9.回文数
题目难度：easy
思路：
将数字转化为字符串存入数组，然后双指针一个指向头部一个指向尾部，遍历数组对比。如果左指针下标小于右指针下标时即符合遍历条件，然后输出结果即可。
代码：
```
bool isPalindrome(int x) {
    int right = 0;
    int left = 0;
    char a[100];
    sprintf(a, "%d", x);
    right = strlen(a) - 1;
    for (right, left;left < right;left++, right--) {
        if (a[left] != a[right]) {
            return false;
        }
    }
    return true;
}
```
10.字符串中的第一个唯一字符
题目难度：easy
思路：
遍历将每个字符出现的次数进行计算，第二次遍历找到次数统计为1的，找到下标，输出即可。
代码：
```
int firstUniqChar(char* s) {
    int str[26]={0};
    int length=strlen(s);
    int result=0;
    //遍历每个字母出现的次数
    for(int i=0;i<length;i++){
        str[s[i]-'a']++;
    }
    for(int i=0;i<length;i++){
        if(str[s[i]-'a']==1){
            result=i;
            return result;
        }
    }
    return -1;
}
```
11.找到稳定山的下标
题目难度：easy
思路：
先初始化然后遍历，找到符合条件的存入结果数组，输出数组即可。
代码：
```
int* stableMountains(int* height, int heightSize, int threshold,
                     int* returnSize) {
    int* result = (int*)malloc((heightSize - 1) * sizeof(int));
    *returnSize = 0;
    for (int i = 1; i < heightSize; i++) {
        if (height[i - 1] > threshold) {
            result[*returnSize] = i;
            (*returnSize)++;
        }
    }
    return result;
}
```
12.判断国际象棋棋盘中一个格子的颜色
题目难度：easy
思路：
观察棋盘可以发现横纵轴的和加起来是奇数则为黑色，返回false，不然返回true
代码：
```
//1812判断国际象棋棋盘中一个格子的颜色
bool squareIsWhite(char *coordinates)
{
    // 找到两个数字加起来为奇数为黑，反之为白
    int result = 0;
    result = coordinates[0] - 'a' + coordinates[1];
    if (result % 2 == 0)
    {
        return true;
    }
    else
    {
        return false;
    }
}
```
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
题目难度：easy<br>
思路：<br>
类似于斐波那契数列，第三项开始结果为前2项数组之和。<br>
```
//70爬楼梯
int climbStairs(int n)
{
    if (n == 1)
    {
        return 1;
    }
    if (n == 2)
    {
        return 2;
    }
    int i = 0;
    int dp[n + 1] ;
    dp[1] = 1;
    dp[2] = 2;
    if (n > 2)
    {
        for (int i = 3; i <= n; i++)
        {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
    }
    return dp[n];
}
```
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
## 数学
1.三除数
题目难度：easy<br>
思路：<br>
遍历 找能够被他本体相除的数，统计这个数是否为3即可。<br>\
代码：
```
//1952三除数
bool isThree(int n) {
    int count=0;
    if(n<=3){
        return false;
    }
    for(int i=1;i<=n;i++){
        if(n%i==0){
            count++;
        }
    }   
    if(count==3){
        return true;
    }else{
        return false;
    }
}
```
## 额外题目
1.有多少小于当前数字的数字<br>
2.有效的山脉数组<br>
3.独一无二的出现次数<br>
4.移动零<br>
5.旋转数组<br>
6.寻找数组的中心索引<br>