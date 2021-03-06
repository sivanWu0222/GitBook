# [268. 缺失数字](https://leetcode-cn.com/problems/missing-number/)



## 方法一：快排 + 二分

时间复杂度：O(N*logN)

思路：快排之后进行二分，查找到缺失的数字并返回

## 方法二：遍历一次数组



1. 遍历的时候，记录该数组的和，同时动态维护最小值和最大值，
2. 遍历完成之后，首先检查最小值是否为0，如果不是直接返回0，之后做如下操作
   1. 如果数组的和 != [最小值，最大值]这个闭区间范围的和，那么我们直接做差返回即可
   2. 如果等于则说明缺失最后一个N，直接返回len(nums)即可


## 【推荐】方法三：利用异或的性质 x ^ x = 0

思路：利用异或的性质 x ^ x = 0 ，我们构造一个0-N的数组(不存在缺失数字)直接与传入的数组进行异或，此时就已经转换为136题，数组中某个数出现了1次，其他数都出现了两次，只不过我们这里是两个数组。

**构造一个数组(包含[0,n]之间的所有数字，将传入的数组与这个数组中所有元素异或，其实走到这里就等价于136题中的某个数出现了1次，其他数都出现了两次)**


> 执行用时：16 ms, 在所有 Go 提交中击败了97.39%的用户
> 内存消耗：6.3 MB, 在所有 Go 提交中击败了7.66%的用户

```go
func missingNumber(nums []int) int {
	xorRet := 0
	for i := 0; i < len(nums); i++ {
		xorRet ^= (nums[i] ^ i)
	}
	//因为最后传入的数组没有那个下标数
	return xorRet ^ len(nums)
}
```

