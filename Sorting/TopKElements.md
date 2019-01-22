### Partial Sorting:

#### Application: Find top K elements in a list
Finding top K elements sounds very simple and intuitive i.e. we can directly sort the list and return first K elements but the question here is, do we really need to sort the whole list? can we somehow magically get the first K elements without sorting the whole list? answer is, **Yes**, we can. And there are several ways to do it. We will talk about different approaches here and see which one is better in terms of efficiency.

Let's go through them one by one:

#### Using Max heap (HeapSort)

The idea is to iterate over the list and start building the max heap and keep track of the size of the max heap. Whenever the size of the max heap is greater than K, delete the largest element i.e. root of the tree. Once, the iteration is over, we will have a max heap tree with K nodes. Keep deleting the root nodes until there are no more nodes left in the tree. 

```python
class TreeNode():
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

class Heap():
    def __init__(self, nums=[]):
        self.nums = [None] + nums
        for i in range(len(self.nums) - 1, 0, -1):
            self._heapify(i)
      
    def _heapify(self, index):
        largest = index
        leftChild = 2 * index
        rightChild = (2 * index) + 1
        if leftChild < len(self.nums) and self.nums[leftChild] > self.nums[largest]:
            largest = leftChild
         
        if rightChild < len(self.nums) and self.nums[rightChild] > self.nums[largest]:
            largest = rightChild
        
        if largest != index:
            self.nums[largest], self.nums[index] = self.nums[index], self.nums[largest]
            self._heapify(largest)
  
    def heapSort(self):
        res = []
        while len(self.nums) > 1:
            res.append(self.delete())
         
        return res[::-1]
    
    def insert(self, val):
        """Inserts the element into the right position using filter-up algorithim"""
        self.nums.append(val)
        if len(self.nums) == 2:
            return

        parent = (len(self.nums) - 1) / 2
        i = len(self.nums) - 1
        while parent > 0:
            if self.nums[parent] < val:
                self.nums[parent], self.nums[i] = self.nums[i], self.nums[parent]
                i = parent
                parent = i / 2
            else:
                break
    
    def delete(self):
        """Deletes and returns the root of the tree."""
        if len(self.nums) <= 1:
            return
        self.nums[1], self.nums[- 1] = self.nums[- 1], self.nums[1]
        res = self.nums.pop()
        self._heapify(1)
        return res

   
    def getMaxEle(self):
        if len(self.nums) > 1:
            return self.nums[1]

        return
    
    def buildTree(self):
        pass
  
```
Above is the implementation of `MaxHeap` from scratch which supports `Insertion, Deletion, getMaxEle & HeapSort`.
Input: arr = `[2,4,5,1,0,6,7,18,12,17]`, K = `4`
##### Using HeapSort
```python
h = Heap(arr)
h.heapSort()
h.nums[:K]
```
Above method has a Time Complexity of O(nlogn) (i.e. to build to MaxHeap tree) + O(nlogn) (i.e. to Delete n elements) and O(n) space complexity.

##### Build only K size heap
```pyhton
h = Heap()
for n in arr:
    if K:
        h.insert(n)
        K -= 1
    else:
        maxEle = h.getMaxEle()
        if maxEle and n < maxEle:
            h.delete()
            h.insert(n)

h.heapSort()    
```
Time Complexity: O(nlogn) (i.e. to build to MaxHeap tree) + O(nlogn) (i.e. to Delete n elements)  
Space Complexity: O(K)

#### Using Min Heap




