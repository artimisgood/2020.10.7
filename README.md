# 2020.10.7————三数之和
## 题目
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。



示例：
```
给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```
## 解题
### 语言
java
### 思路
三重循环解决问题，为了减少重复，我们枚举的三元组 (a, b, c) 满足 a≤b≤c,对于每一重循环而言，相邻两次枚举的元素不能相同，否则也会造成重复。

这样子是三重循环，时间复杂度还是很高，我们发现当我们找到前两个数字的时候，由于是相加为零而且顺序排列，第三个数字能用前两个的相关关系表示出来。我们设置第三个数的从右向左的指针。
### 代码
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);//给数组排序
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        //枚举a
        for(int first = 0;first<n;++first){
            //需要和上次的数不相同
            if(first>0&&nums[first]==nums[first-1]){
                continue;
            }
            //c对应的指针指向数组最右
            int third = n-1;
            int target = -nums[first];
            //枚举b
            for(int second = first+1;second<n;++second){
                //需要和上次的数字不同
                if(second>first+1&&nums[second]==nums[second-1]){
                    continue;
                }
                //确保b指针在a指针左侧
                while(second<third&&nums[second]+nums[third]>target){
                    --third;
                }
                //指针重合，b后续增加，那就不会出现b<c的情况了
                if(second==third){
                    break;
                }
                if(nums[second]+nums[third]==target){
                    List<Integer> list = new ArrayList<Integer>();
                    list.add(nums[first]);
                    list.add(nums[second]);
                    list.add(nums[third]);
                    ans.add(list);
                }
            }
        }
        return ans;
    }
}
```
