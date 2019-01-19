### Find top K elements in a list:
Finding top K elements sounds very simple and intuitive i.e. we can directly sort the list and return first K elements but the question here is, do we really need to all the whole list? can we somehow magically get the first K elements without sorting the whole list? answer is, **Yes**, we can. And there are several ways to do it. We will talk about different approaches here and see which one is better in terms of efficiency.

Let's go through them one by one:

#### Using Max heap

The idea is to start building the max heap and whenver the size of the max heap is greater than K, delete the largest element i.e. root of the tree.  