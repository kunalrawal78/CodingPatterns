# 📚 CodingPatterns: Java Collections Functions

A curated set of Java coding patterns using core collection classes — `HashSet`, `HashMap`, `ArrayList`, and `LinkedList`. Each section includes purpose, common methods, and DSA-style examples.

---

## 🔹 HashSet in Java

**Purpose:** Stores unique elements with no duplicates. Offers constant-time operations for `add`, `remove`, and `contains`.

### ✅ DSA Problem: First Duplicate in Array

```java
import java.util.HashSet;
public class FirstDuplicate {
    public static Integer findFirstDuplicate(int[] nums) {
        HashSet<Integer> seen = new HashSet<>();
        for (int num : nums) {
            if (seen.contains(num)) return num;
            seen.add(num);
        }
        return null;
    }
    public static void main(String[] args) {
        int[] arr = {3, 1, 4, 2, 5, 3, 2};
        System.out.println("First duplicate: " + findFirstDuplicate(arr));
    }
}
🔧 Common Methods
add(element)

contains(element)

remove(element)

size()

isEmpty()

🔹 HashMap in Java
Purpose: Stores key-value pairs. Ideal for counting, mapping, and indexing.

✅ DSA Problem: Frequency Counter
java
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
🔧 Common Methods
put(key, value)

get(key)

getOrDefault(key, default)

containsKey(key)

remove(key)

keySet(), values(), entrySet()

🔍 HashSet vs HashMap
Feature	HashSet	HashMap
Structure	Stores only values	Stores key-value pairs
Use Case	Uniqueness check	Counting, mapping, caching
Backed By	Internally uses HashMap	Native implementation
🔹 ArrayList in Java
Backed by: Dynamic array Best for: Fast random access, frequent reads

✅ DSA Problem: Remove Duplicates from List
java
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
🔧 Common Methods
add(element)

add(index, element)

get(index)

set(index, element)

remove(index)

size()

contains(element)

clear()

🔹 LinkedList in Java
Backed by: Doubly linked list Best for: Frequent insertions/deletions

✅ DSA Problem: Simple Queue Implementation
java
import java.util.LinkedList;
public class SimpleQueue {
    public static void main(String[] args) {
        LinkedList<Integer> queue = new LinkedList<>();
        queue.addLast(10);
        queue.addLast(20);
        queue.addLast(30);
        System.out.println("Dequeued: " + queue.removeFirst());
        System.out.println("Front element: " + queue.peekFirst());
        System.out.println("Current queue: " + queue);
    }
}
🔧 Common Methods
addFirst(element)

addLast(element)

removeFirst()

removeLast()

peekFirst()

peekLast()

get(index)


🔹 HashSet Revisited: Duplicate Check
✅ DSA Problem: Check for Duplicates
java
import java.util.HashSet;
public class ContainsDuplicate {
    public static boolean hasDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int num : nums) {
            if (!set.add(num)) return true;
        }
        return false;
    }
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 2};
        System.out.println("Has duplicate: " + hasDuplicate(arr));
    }
}
🔧 Common Methods
add(element)

contains(element)

remove(element)

size()

clear()

isEmpty()

🔧 Collections Utility Methods
Collections.sort(list)

Collections.reverse(list)

Collections.max(list)

Collections.min(list)

Collections.frequency(list, element)
