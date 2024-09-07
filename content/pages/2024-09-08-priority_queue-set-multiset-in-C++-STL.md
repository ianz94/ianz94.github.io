+++
title = 'priority_queue / set / multiset in C++ STL - Which One to Choose?'
date = 2024-09-08T00:19:48+08:00
draft = false
+++

`priority_queue`, `set` and `multiset` are all useful for storing elements in a sorted order. All you have to do is pushing data into theses containers, they all will help you manage your data in an ordered manner in some way.

### Commonalities

- Automatic Sorting: Each of these containers helps you manage data that is (at least partially) ordered.
- Logarithmic Complexity: They provide logarithmic time complexity `O(log n)` for insertion and removal operations.
- Generic: They can be used with any data type as long as the type supports comparison operators (`<`, `>`, etc.).
- Custom Comparators: You can define custom sorting orders using comparators for `set`, `multiset`, and `priority_queue`.

---

### `priority_queue`: Efficient Access to the Largest (or Smallest) Element

A `priority_queue` is a container adapter that provides constant-time access `O(1)` to the largest (or smallest) element, depending on whether it’s implemented as a **max-heap** (default) or a **min-heap**. Internally, it uses a **binary heap** to maintain partial order, meaning **only the top element is guaranteed to be sorted**.

**Characteristics:**
- No Full Order: Only the top element is guaranteed to be the largest (or smallest) in the queue.
- Duplicates: Supports duplicates.
- Heap Property: Provides fast `O(1)` access to the top element and `O(log n)` for insertion and removal.
- Custom Comparator: Can be used to define min-heaps or other custom orderings.

**Use Cases:**
- [Top-k Problems](https://leetcode.com/problems/top-k-frequent-elements/): Ideal for finding the largest or smallest `k` elements from a dataset.
- Priority-based Scheduling: Used in applications like event-driven simulations or job scheduling where tasks with the highest priority are processed first.
- Algorithms: Commonly used in algorithms like Dijkstra’s shortest path and Prim’s minimum spanning tree.

**Code Example:**
```cpp
#include <iostream>
#include <queue>
#include <vector>

int main() {
    std::priority_queue<int> pq;

    pq.push(10);
    pq.push(5);
    pq.push(20);

    std::cout << "Top element: " << pq.top() << std::endl; // Output: 20

    pq.pop();
    std::cout << "Top element after pop: " << pq.top() << std::endl; // Output: 10

    return 0;
}
```

---

### `set`: A Sorted Collection with Unique Elements

A `set` is an associative container that stores unique elements in a strictly sorted order. It is typically implemented using a **balanced binary search tree** (like a red-black tree), which provides logarithmic time complexity for insertion, removal, and lookup.

**Characteristics:**
- Sorted: All elements are stored in ascending (or custom) order.
- Uniqueness: Each element in a `set` is unique. Duplicate elements are not allowed.
- Iterator Support: You can iterate over the elements in sorted order.
- Logarithmic Search: Allows efficient searching for elements with `O(log n)` complexity.

**Use Cases:**
- Unique Sorted Elements: Use `set` when you need to maintain a collection of unique elements that need to be accessed in sorted order (e.g., maintaining a list of unique event timestamps).
- Efficient Lookups: Ideal when you need to frequently check for the presence of an element in a sorted collection (e.g., membership testing in a dictionary or symbol table).
- Range Queries: Since elements are stored in order, `set` is useful for problems involving range queries or ordering.

**Code Example:**
```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s;

    s.insert(10);
    s.insert(5);
    s.insert(20);
    s.insert(5);  // Duplicate, will not be inserted

    std::cout << "Elements in the set: ";
    for (int x : s) {
        std::cout << x << " "; // Output: 5 10 20
    }
    std::cout << std::endl;

    return 0;
}
```

---

### `multiset`: A Sorted Collection with Duplicate Elements Allowed

A `multiset` is similar to a `set`, but it allows **duplicate elements**.

**Use Cases:**
- Counting Elements: Useful when you need to store elements in sorted order and need to count how many times each element appears.
- Sorted Multi-collections: When you need to maintain order in a collection that may have duplicate values (e.g., processing and storing frequency of occurrences of values in a dataset).
- Range Queries: Like `set`, `multiset` is also useful for range queries where duplicates are allowed.

#### Code Example:
```cpp
#include <iostream>
#include <set>

int main() {
    std::multiset<int> ms;

    ms.insert(10);
    ms.insert(5);
    ms.insert(20);
    ms.insert(5);  // Duplicate, will be inserted

    std::cout << "Elements in the multiset: ";
    for (int x : ms) {
        std::cout << x << " "; // Output: 5 5 10 20
    }
    std::cout << std::endl;

    return 0;
}
```

---

### Key Differences Between `priority_queue` / `set` / `multiset`

| Feature                        | `priority_queue`                      | `set`                                      | `multiset`                                   |
|---------------------------------|---------------------------------------|--------------------------------------------|----------------------------------------------|
| **Order**                       | Only top element is accessible in sorted order (heap). | All elements are stored in sorted order.    | All elements are stored in sorted order.     |
| **Duplicates**                  | Duplicates allowed.                   | No duplicates allowed.                     | Duplicates allowed.                          |
| **Access Complexity**           | `O(1)` for top element, `O(log n)` for insertion/removal. | `O(log n)` for insertion, removal, search. | `O(log n)` for insertion, removal, search.   |
| **Iterator Support**            | No iterator support (cannot iterate). | Full iterator support (sorted order).      | Full iterator support (sorted order).        |
| **Use Case**                    | Efficient access to largest/smallest element (heap-based algorithms). | Unique sorted collections (without duplicates). | Sorted collections with duplicates allowed.  |

---

### Summary

- Use `priority_queue` when you only care about efficiently accessing the top element (e.g., largest or smallest) and don’t need full order traversal.
- Use `set` when you need a sorted collection of unique elements and want to perform efficient lookups and ordered traversals.
- Use `multiset` when you need a sorted collection but allow duplicate elements, which is useful for frequency counting or range queries with duplicates.

