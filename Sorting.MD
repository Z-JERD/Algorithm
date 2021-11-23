# 二分查找

## 复杂度
    
    时间复杂度： O(logn) 最好 O(1)
    
## 实现方式
    
    循环：
        
        def binary_search(data, target):
        
            left, right = 0, len(data) - 1
        
            while left <= right:
        
                mid = left + (right - left) // 2  # (left + right) // 2 可能造成溢出
        
                if data[mid] == target:
        
                    return mid
        
                elif data[mid] > target:
        
                    right = mid - 1
        
                elif data[mid] < target:
        
                    left = mid + 1
        
            return -1
    
    递归：
        def binary_recursive(data, target, left=0, right=None):
        
            if right is None:
        
                right = len(data) - 1
        
            if left <= right:
        
                mid = left + (right - left) // 2
        
                if data[mid] == target:
                    return mid
        
                elif data[mid] > target:
                    binary_recursive(data, target, left, mid - 1)
        
                elif data[mid] < target:
        
                    binary_recursive(data, target, mid + 1, right)
        
            return -1
            
# 排序算法

    参考文档：https://mp.weixin.qq.com/s/IAZnN00i65Ad3BicZy5kzQ
              https://mp.weixin.qq.com/s?__biz=MzUyNjQxNjYyMg==&mid=2247484184&idx=1&sn=62965b401aa42107b3c17d1d8ea17454
 
# 选择排序

## 本质：
    
    选择排序就是不断地从未排序的元素中选择最大（或最小）的元素放入已排好序的元素集合中
    
    过程描述：
        
        首先，找到数组中最小的那个元素，将它和数组的第一个元素交换位置
        其次，在剩下的元素中找到最小的元素，将它与数组的第二个元素交换位置。
        如此往复
        
## 复杂度
    
    时间复杂度：O(n2)
    
    空间复杂度：O(1) 
    
    排序方式: 原地排序
    
    非稳定排序：
        
        选择元素之后会发生交换操作，所以有可能把前面的元素交换到后面，所以不是稳定的排序
        
        排序前： [3(1), 5, 3(2), 2]
        
        排序后:  [2, 5, 3(2), 3(1)]
        
## 实现方式

    def func(info):
        
        for index in range(0, len(info)-1):
    
            min_index, initial_data = index, info[index]
    
            for after_index in range(index+1, len(info)):
    
                if info[after_index] < info[min_index]:
                    min_index = after_index
    
            info[index], info[min_index] = info[min_index], initial_data

# 插入排序

## 本质：
    
    将数据插入到有序数据中合适的位置，其余所有元素在插入之前都要向右移动一位
    
    过程描述：
        
        从数组中第2个元素开始抽取元素
        
        把它与左边第一个元素比较，如果左边第一个元素比它大，则继续与左边第二个元素比较下去，直到遇到不比它大的元素，然后插到这个元素的右边
        
        继续选取第3，4，….n个元素,重复步骤 2 ，选择适当的位置插入。
        
## 复杂度
   
    时间复杂度：O(n2)
    
    空间复杂度：O(1) 
    
    排序方式: 原地排序
    
    稳定排序:
        
        两个数相等的话，不会进行移动，前后两个数的次序不会发生改变
        
        
 ## 实现方式：
    
     def func(info):
        
        for index in range(1, len(info)):

            current_data = info[index]

            bf_index = index - 1

            while bf_index >= 0 and info[bf_index] > current_data:

                info[bf_index + 1] = info[bf_index]

                bf_index -= 1

            info[bf_index+1] = current_data
            
        return info


# 冒泡排序

## 本质：
    
    把第一个元素与第二个元素比较，如果第一个比第二个大，则交换他们的位置。接着继续比较第二个与第三个元素，
    如果第二个比第三个大，则交换他们的位置….
    
    除去最右的元素，我们对剩余的元素做同样的工作，如此重复下去，直到排序完成。
    
## 复杂度

    时间复杂度：O(n2)  最优：O(n) 列表已经是有序状态
    
    空间复杂度：O(1) 
    
    原地排序 
    
    稳定排序
    
## 实现方式
    
    def func(info):
       
        for index in range(0, len(info) - 1):
    
            for nx_index in range(0, len(info) - 1 - index):
    
                if info[nx_index] > info[nx_index + 1]:
                    info[nx_index], info[nx_index + 1] = info[nx_index + 1], info[nx_index]
    
        return info

# 快速排序

## 本质：
    
    从数组中选择一个元素（中轴元素），然后把数组中所有小于中轴元素的元素放在其左边，所有大于或等于中轴元素的元素放在其右边
    
    接着通过递归的方式，让中轴元素左边的数组和右边的数组也重复同样的操作，直到数组的大小为1，此时每个元素都处于有序的位置
    
## 过程描述
    
    1. 用第一个元素充当主元
    
    2. 令变量i = left + 1，j = right。然后让 i 和 j 从数组的两边向中间扫描
        
    3. i 向右遍历的过程中，如果遇到大于或等于主元的元素时，则停止移动，j向左遍历的过程中，如果遇到小于或等于主元的元素则停止移动。
    
    4. 当i和j都停止移动时，如果这时i < j，则交换 i, j 所指向的元素。
    
    5. 继续向中间遍历，直到i >= j， 最后在把主元与 j 指向的元素交换
    
    6. 这个时候，j 左边的元素一定小于或等于主元，而右边则大于或等于主元。到此，分割调整完毕

## 复杂度
    
    时间复杂度：O(nlogn) 最坏：O(n2)
            
            最好的情况就是每次分割都能够从数组的中间分割了，这样分割logn次就行了，此时的时间复杂度为O(nlogn)
            
            
            极端的情况，每次分割的时候，主元左边的元素个数都为0，而右边都为n-1个。这个时候，就需要分割n次了。
            而每次分割整理的时间复杂度为O(n)，所以最坏的时间复杂度为O(n2)
    
    空间复杂度：O(logn)
    
    非稳定排序
    
    原地排序

## 实现方式

    def partition(data, left, right):
    
        initial_index = left
        tmp = data[initial_index]
    
        while left < right:
    
            while left < right and data[right] > tmp:
    
                right -= 1
    
            while left < right and data[left] <= tmp:
    
                left += 1
    
            if left < right:
    
                data[left], data[right] = data[right], data[left]
    
        data[initial_index], data[left] = data[left], tmp
    
        return left
    
    
    def quick_sort(data, left, right):
    
        if left < right:
    
            mid = partition(data, left, right)
    
            quick_sort(data, left, mid - 1)
    
            quick_sort(data, mid + 1, right)
    
    
    li = [4, 1, 8, 2, 7, 6, 3]
    quick_sort(li, 0, len(li) - 1)

# 归并排序

## 本质：
   
    将待排序的数分成两半后排好序，然后再将两个排好序的序列合并成一个有序序列
    
    通过递归的方式将大的数组一直分割，直到数组的大小为 1，此时只有一个元素，那么该数组就是有序的了，
    之后再把两个数组大小为1的合并成一个大小为2的，再把两个大小为2的合并成4的 ….. 直到全部小的数组合并起来。

## 复杂度

    时间复杂度：O(nlogn)  
    
    空间复杂度：O(n)  
    
    稳定排序:
        
        因为在合并的时候，如果相等，选择前面的元素到辅助数组  
    
    非原地排序
    
    
## 实现方式

    def merge(li_1, li_2):
    
        result = []
    
        while li_1 and li_2:
    
            if li_1[0] <= li_2[0]:
                result.append(li_1.pop(0))
            else:
                result.append(li_2.pop(0))
    
        if li_1:
    
            result += li_1
    
        if li_2:
            result += li_2
    
        return result
    
    
    def merge_sort(data):
        """
        归并排序
        """
        if len(data) <= 1:
            return data
    
        mid = len(data) // 2
    
        return merge(merge_sort(data[:mid]), merge_sort(data[mid:]))
    
    
    if __name__ == '__main__':
    
        arr = [17, 56, 71, 38, 61, 62, 48, 28, 57, 42]
    
        arr_new = merge_sort(arr)
