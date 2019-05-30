# Leetcode 复习
最近在做Array的题，在这里会把做过的题总结下，当作复习和以后看的时候方便

- [Leetcode复习](#Leetcode-复习)
	- [27 Remove Element](#remove-element)
	- [1.1 Reference and Pointer](#reference-and-pointer)
		- [1.1.1 Reference](#reference)
		- [1.1.2 Pointer](#Pointer)
	- [1.2 Const Keyword](#const-keyword)
		- [1.2.1 const pointer](#const-pointer-and-pointer-to-const)
		- [1.2.2 const expression](#const-expression)
	- [1.3 Typedef](#type-def)


## remove element
[Remove Element](https://leetcode.com/problems/remove-element/)
难度:Easy. 
Given an array nums and a value val, remove all instances of that value in-place and return the new length.
Do not allocate extra space for another array, you must do this by **modifying the input array** in-place with O(1) extra memory.
The order of elements can be changed. It doesn't matter what you leave beyond the new length. 
Example 1:
Given nums = [3,2,2,3], val = 3,
Your function should return length = 2, with the first two elements of nums being 2.
It doesn't matter what you leave beyond the returned length.
Example 2:
Given nums = [0,1,2,2,3,0,4,2], val = 2,
Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.
Note that the order of those five elements can be arbitrary.
It doesn't matter what values are set beyond the returned length.
这题要求把数字删除，而且要直接在array上面改，不用新增其他的东西，而且最后返回前面有效数字的个数。
我的做法是用两个指针，一个记录当前扫过去的个数，一个记录最后有效的index。
每次找到要删除的数字，直接把后面的数字放到前面，并且后面的指针往前移动，不过这个时候不能直接增加前面的指针，因为有可能后面放过来的数也是需要删除的。
只有在不删除当前数字的情况下，才增加前面的指针。
代码如下：
```C++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        if (nums.empty()) {return 0;}
        int j = nums.size() - 1;
        int i = 0;
        while (i <= j) {
            if (nums[i] == val) {
                swap(nums[i], nums[j--]);
            }
            if (nums[i] != val) {
                i++;
            }
        }
        return nums.size() - (nums.size() - j - 1);
    }
};
```