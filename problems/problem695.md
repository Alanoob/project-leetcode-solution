## Problem 521: Max Area of Island

problem: [Max Area of Island](https://leetcode.com/problems/max-area-of-island/description/)

### Solution

- [Python](../python/problem695.py)

- [C++](../cpp/problem695.cpp)

- [Swift](../swift/problem695.swift)

### Discussion

**DFS Solution**

Typically this problem can be solve by DFS search. See [Leetcode official solution](https://leetcode.com/problems/max-area-of-island/solution/) for an example. The DFS method costs O(M*N) space, O(MxN) time.

**UFSet solution**

But here we present a solution use 2-d Union-Find set. See [C++ Solution](../cpp/problem695.cpp) for an example. As tested, this is faster than DFSs, and most importantly, this cost no extra space.

To enable the 2-d UFSet to work:
- We use 0 to represent water, use 1 to represent original island. This is consistent with the input matrix. For example the following one:
    ```txt
    0   0   1   0   1
    0   0   1   1   1
    0   1   1   0   0
    1   1   0   0   0
    0   1   1   1   1
    ```
- Positive value indicates the element is a root, and the value of it represents the area attach this tree.
- Negative value indicates the element is not root, and the value of it indicate the position index of the root (see below for 1-d index definition).
- the parent pointer index (i,j) in for 2-d matrix need to be converted to 1-d index. The conversion can be done by the following methods:
    ```c++
    void id2coord(int id, int &x, int &y){
        x = (-id - 1)/ncol; y = (-id - 1)%ncol;
    }
    int coord2id(int x, int y){
        return -(x*ncol + y + 1);
    }
    ```
- In the solution, we use the loop only once, to merge the connected component. Finally we find the maximum tree. The matrix after the first run is
    ```txt
    0   0   13  0   -3
    0   0   -3  -3  -5
    0   -3  -3  0   0
    -3  -3  0   0   0
    0   -3  -3  -3  -3
    ```
    The maximal element 13 now is the answer.






