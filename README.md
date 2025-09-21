📚 Java Collections: A Guide to Core Data Structures
This guide provides a curated set of Java coding patterns using the core collection classes: HashSet, HashMap, ArrayList, and LinkedList. Each section outlines the purpose of the class, its common methods, and practical examples from Data Structures and Algorithms (DSA) problems.

🔹 HashSet in Java
A HashSet is a collection that stores unique elements with no duplicates. It offers constant-time average performance for basic operations like add, remove, and contains, making it highly efficient for checking for the existence of an element. This is because it uses a hash table internally.

💡 Purpose & Use Cases
Uniqueness Check: Ideal for quickly determining if an element is present in a collection or for removing duplicates.

Membership Testing: Used to efficiently check if an element belongs to a set of items.

✅ DSA Problem: First Duplicate in Array
This problem finds the first element that appears more than once in an array. A HashSet is perfect for this as we can iterate through the array and check if an element has been "seen" before in constant time.

import java.util.HashSet;

public class FirstDuplicate {
    public static Integer findFirstDuplicate(int[] nums) {
        HashSet<Integer> seen = new HashSet<>();
        for (int num : nums) {
            if (seen.contains(num)) {
                return num; // Found the first duplicate
            }
            seen.add(num);
        }
        return null; // No duplicates found
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 4, 2, 5, 3, 2};
        System.out.println("First duplicate: " + findFirstDuplicate(arr)); // Output: 3
    }
}



**🔧 Common Methods
add(element): Adds an element to the set. Returns false if the element already exists.
contains(element): Checks if the set contains the specified element.
remove(element): Removes the specified element from the set.
size(): Returns the number of elements in the set.
isEmpty(): Checks if the set is empty.**
-------------------------------------------------------------------------------------------------
.

🔹 HashMap in Java
A HashMap stores data as key-value pairs. It's a powerful tool for creating mappings, performing counts, and caching data. Like HashSet, it provides constant-time average performance for put and get operations.

💡 Purpose & Use Cases
Frequency Counter: Counting the occurrences of items in a list or array.

Mapping & Caching: Storing associations between different data points (e.g., student IDs to names).

Indexing: Creating a quick lookup table.

✅ DSA Problem: Frequency Counter
This problem counts the frequency of each element in an array. A HashMap is the ideal choice as we can map each unique number (key) to its count (value).

import java.util.HashMap;

public class FrequencyCounter {
    public static void countFrequencies(int[] nums) {
        HashMap<Integer, Integer> freqMap = new HashMap<>();
        for (int num : nums) {
            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        }

        for (int key : freqMap.keySet()) {
            System.out.println("Element: " + key + ", Frequency: " + freqMap.get(key));
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 2, 3, 1, 4, 2};
        countFrequencies(arr);
    }
}


**🔧 Common Methods
put(key, value): Associates the specified value with the specified key.
get(key): Returns the value to which the specified key is mapped.
getOrDefault(key, default): Returns the value for the key or a default value if the key isn't found.
containsKey(key): Checks if the map contains the specified key.
remove(key): Removes the mapping for the specified key.
keySet(), values(), entrySet(): Provides different views of the map's contents**



🔍 HashSet vs HashMap
Feature	HashSet	HashMap
Structure	Stores only values	Stores key-value pairs
Use Case	Uniqueness, membership check	Counting, mapping, caching
Backed By	Internally uses a HashMap	Native implementation

🔹 ArrayList in Java
An ArrayList is a resizable array that can grow or shrink as needed. It's backed by a dynamic array, making it excellent for fast random access of elements by their index.

💡 Purpose & Use Cases
Fast Reads: Perfect when you need to frequently access elements at a specific index.

Dynamic Sizing: Useful when the number of elements isn't known beforehand.

✅ DSA Problem: Remove Duplicates from List
This problem shows how to remove duplicate elements from an ArrayList while preserving the order of the first occurrence. We use a HashSet as a helper to efficiently track which elements have already been added to our result list.

import java.util.ArrayList;
import java.util.HashSet;

public class RemoveDuplicates {
    public static ArrayList<Integer> removeDuplicates(ArrayList<Integer> list) {
        HashSet<Integer> seen = new HashSet<>();
        ArrayList<Integer> result = new ArrayList<>();
        for (int num : list) {
            if (!seen.contains(num)) {
                seen.add(num);
                result.add(num);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        ArrayList<Integer> nums = new ArrayList<>();
        nums.add(1); nums.add(2); nums.add(2); nums.add(3); nums.add(1);
        System.out.println("After removing duplicates: " + removeDuplicates(nums));
    }
}


**🔧 Common Methods
add(element): Appends an element to the end.
add(index, element): Inserts an element at a specific index.
get(index): Retrieves an element by its index. This is a constant-time operation.
set(index, element): Replaces an element at a specific index.
remove(index): Removes an element at a specific index. This is a linear-time operation.
size(): Returns the number of elements.**
--------------------------------------------------------------------------------------------------

🔹 LinkedList in Java
A LinkedList is a data structure that stores elements in nodes, where each node holds a reference to the next (and previous) node. It's backed by a doubly linked list, making it highly efficient for frequent insertions and deletions at the beginning or end.

💡 Purpose & Use Cases
Queue & Stack: Perfect for implementing queues (FIFO - First-In, First-Out) or stacks (LIFO - Last-In, First-Out).

Frequent Modifications: Ideal when your program requires frequent additions or removals of elements, especially at the list's ends.

✅ DSA Problem: Simple Queue Implementation
This example demonstrates how a LinkedList can serve as a simple queue. Elements are added to the end (addLast) and removed from the beginning (removeFirst).


import java.util.LinkedList;

public class SimpleQueue {
    public static void main(String[] args) {
        LinkedList<Integer> queue = new LinkedList<>();
        
        // Enqueue operations
        queue.addLast(10); 
        queue.addLast(20);
        queue.addLast(30);

        // Dequeue operations
        System.out.println("Dequeued: " + queue.removeFirst()); // Output: 10
        System.out.println("Front element: " + queue.peekFirst()); // Output: 20
        System.out.println("Current queue: " + queue); // Output: [20, 30]
    }
}



🔧 Common Methods
addFirst(element): Inserts an element at the beginning.
addLast(element): Appends an element to the end.
removeFirst(): Removes and returns the first element.
removeLast(): Removes and returns the last element.
peekFirst(): Retrieves, but does not remove, the first element.
peekLast(): Retrieves, but does not remove, the last element.
get(index): Warning: This is a linear-time operation, as the list must be traversed from the start or end.
---------------------------------------------------------------------------------------------
🔧 Collections Utility Methods
The java.util.Collections class provides a set of powerful static utility methods that can be used with various collections.
Collections.sort(list): Sorts the elements in a list.
Collections.reverse(list): Reverses the order of elements in a list.
Collections.max(list): Returns the maximum element in a collection.
Collections.min(list): Returns the minimum element in a collection.
Collections.frequency(list, element): Counts the number of times an element appears in a list.
