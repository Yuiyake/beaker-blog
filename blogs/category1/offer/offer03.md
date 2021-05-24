---
title: 剑指offer 03 重复数字
date: 2021-05-22
categories: 
- 剑指offer
---
## 找出数组中重复的数字。
- 题目
  - 在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，
    但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。


<CodeGroup>
  <CodeGroupItem title="YARN">

```bash:no-line-numbers
yarn
```

  </CodeGroupItem>

  <CodeGroupItem title="NPM" active>

```bash:no-line-numbers
npm install
```

  </CodeGroupItem>
</CodeGroup>


- 哈希表  时间O(n), 空间O(n)
  1. HashSet 特性：    
    a. 不允许有重复元素     
    b. 允许有null      
    c. 无序     
    d. 线程不安全      
  
  2. 语法及使用（更多方法请自行查看api）
---
    - HashSet<String> sites = new HashSet<String>();
    - 添加  用add方法： sites.add("Google");
    - 判断元素是否存在： sites.contains("Taobao")
    - 删除  sites.remove("Taobao");
---

```java
// 哈希表
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> dic = new HashSet<>();
        for(int num : nums) {
            if(dic.contains(num)) return num;
            dic.add(num);
        }
        return -1;
    }
}
```
- 原地交换  时间O(n), 空间O(1)
  1. 分析题目，用数组做的话，可以利用【索引】和【值】建立映射关系
  2. 遍历数组，在第一次遇到这个数字时，将他与索引对应，即nums[i] == i
  3. 如果nums[nums[i]] == nums[i]成立，则代表nums[i]处的索引和nums[i]本身相同，也就是找到了两个一样的值，此时返回。
     否则交换位置。也就是此时的数字是几就到几的索引位置。
  - 看图会好理解点
    <img :src="$withBase('/img/office03-1.png')" alt="foo">

```java
//原地交换
class Solution {
    public int findRepeatNumber(int[] nums) {
        int i = 0;
        while(i < nums.length) {
            if(nums[i] == i) { //第一次的索引值和这个数本身相同，不用换位，索引值+1
                i++;
                continue;
            }
            if(nums[nums[i]] == nums[i]) return nums[i]; //第二次遇到相同的数字，就返回，否则交换位置（下面的代码）
            int tmp = nums[i];
            nums[i] = nums[tmp];
            nums[tmp] = tmp;
        }
        return -1;
    }
}

```
- 补充
  它考察的是程序员的沟通能力，先问面试官要时间/空间需求！
  只是时间优先就用字典，
  还有空间要求，就用指针+原地排序数组，
  如果面试官要求空间O(1)并且不能修改原数组，还得写成二分法！
  ```C
    class Solution:
      def findRepeatNumber(self, nums: List[int]) -> int:
        def count(start,end):
          c,i=0,0
          while i<len(nums):
            if start<=nums[i]<=end:
              c+=1
            i+=1
          return c
      left,right = 0,len(nums)-1
      if right<1:return -1
      while left+1<right:
        mid = (left+right)//2
        if count(left,mid)>mid-left+1:
          right = mid
        else:
          left = mid
      if count(nums[left],nums[left])>1:return nums[left]
      if count(nums[right],nums[right])>1:return nums[right]
      return -1
