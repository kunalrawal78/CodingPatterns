How to identy find questions?
Key words
-overlap
-conflict
-merge
-freetime
-simultaneous usage
-rooms/load/CPU/meetings


56. Merge Intervals
Given an array of intervals where intervals[i] = [starti, endi],
merge all overlapping intervals, and return an array of
 the non-overlapping intervals that cover all the intervals in the input.

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& arr) {
       sort(arr.begin(),arr.end());
        vector<vector<int>>v;
 
        int s1=arr[0][0];
        int e1=arr[0][1];
        for(int i=1;i<arr.size();i++){
            
            if(e1>=arr[i][0]){
                e1=max(e1,arr[i][1]);  
            }
            else{
                v.push_back({s1,e1}); 
                s1=arr[i][0];
                e1=arr[i][1];
            }
            
           
        }
        v.push_back({s1,e1});
        return v;
    }
};
```
questions
Merge Intervals (medium)
Insert Interval (medium)
Intervals Intersection (medium)
Overlapping Intervals
Problem Challenge 1: Minimum Meeting Rooms (hard)
Problem Challenge 2: Maximum CPU Load (hard)
Problem Challenge 3: Employee Free Time (hard)
