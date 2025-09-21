# CodingPatterns

**Java Maps functions**

for (int num : nums) {
    freq.put(num, freq.getOrDefault(num, 0) + 1);
}
**HashSet in Java
Purpose: Stores unique elements, no duplicates, 
and offers constant-time operations for add, remove, and contains.**
------------------------------------------------------------------
import java.util.HashSet;

public class FirstDuplicate {
    public static Integer findFirstDuplicate(int[] nums) {
        HashSet<Integer> seen = new HashSet<>();
        for (int num : nums) {
            if (seen.contains(num)) {
                return num; // First duplicate found
            }
            seen.add(num);
        }
        return null; // No duplicates
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 4, 2, 5, 3, 2};
        System.out.println("First duplicate: " + findFirstDuplicate(arr));
    }
}
----------------------------------------------------------------------------------------------
**🔧 Common HashSet Methods:
add(element) – Adds an element
contains(element) – Checks if present
remove(element) – Removes an element
size() – Returns number of elements
isEmpty() – Checks if empty**

**HashMap in Java
Purpose: Stores key-value pairs, ideal for counting, mapping, and indexing.**
------------------------------------------------------------------------------------------------
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

**🔧 Common HashMap Methods:
put(key, value) – Inserts or updates
get(key) – Retrieves value
getOrDefault(key, default) – Gets value or default
containsKey(key) – Checks if key exists
remove(key) – Removes key-value pair
keySet() – Returns all keys
values() – Returns all values
entrySet() – Returns key-value pairs**

**🔍 Bonus: HashSet vs HashMap
Feature	|HashSet|	HashMap
Structure|	Stores only values|	Stores key-value pairs
Use Case	|Check existence, uniqueness|	Count, map, index, cache
Backed By	| Internally uses HashMap|	Native implementation**

----------------------------------------------------------------------------------------------------
**ArrayList in Java
Backed by: Dynamic array Best for: Fast random access, frequent reads**

✅ DSA Problem: Remove duplicates from a list of integers
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
**🔧 Common ArrayList Methods:
add(element) – Adds at end
add(index, element) – Inserts at index
get(index) – Retrieves element
set(index, element) – Updates element
remove(index) – Removes by index
size() – Returns number of elements
contains(element) – Checks existence
clear() – Empties the list**
-------------------------------------------------------------
**🔹 LinkedList in Java
Backed by: Doubly linked list Best for: Frequent insertions/deletions**
✅ DSA Problem: Implement a simple queue using LinkedList
import java.util.LinkedList;

public class SimpleQueue {
    public static void main(String[] args) {
        LinkedList<Integer> queue = new LinkedList<>();

        // Enqueue
        queue.addLast(10);
        queue.addLast(20);
        queue.addLast(30);

        // Dequeue
        System.out.println("Dequeued: " + queue.removeFirst());

        // Peek
        System.out.println("Front element: " + queue.peekFirst());

        // Print queue
        System.out.println("Current queue: " + queue);
    }
}
**🔧 Common LinkedList Methods:
addFirst(element) – Adds to front
addLast(element) – Adds to end
removeFirst() – Removes from front
removeLast() – Removes from end
peekFirst() – Views front
peekLast() – Views end
get(index) – Access by index (slower than ArrayList)**
<img width="481" height="211" alt="image" src="https://github.com/user-attachments/assets/7f530bd7-586a-4add-bedc-3add17a2bb86" />

---------------------------------------------------------------------------------------------------------
**HashSet
Structure: Backed by a hash table Order: No guaranteed order Use Case: Fast lookup, uniqueness check**

✅ DSA Problem: Check if an array has duplicates
import java.util.HashSet;

public class ContainsDuplicate {
    public static boolean hasDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int num : nums) {
            if (!set.add(num)) return true; // add returns false if already present
        }
        return false;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 2};
        System.out.println("Has duplicate: " + hasDuplicate(arr));
    }
}
**🔧 Common HashSet Methods:
add(element) – Adds element if not present
contains(element) – Checks existence
remove(element) – Deletes element
size() – Number of elements
clear() – Empties the set
isEmpty() – Checks if empty**

**Collections.sort(list)
Collections.reverse(list)
Collections.max(list), Collections.min(list)
Collections.frequency(list, element)**

<img width="275" height="186" alt="image" src="https://github.com/user-attachments/assets/09f945a9-3cb0-4035-a4ca-a1040aaecf3e" />

