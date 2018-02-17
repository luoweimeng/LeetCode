## Problem setting

给一个list， 如何把里面的字符分配到尽量少的子list里，并且每个子list没有重复元素。
比如
['a','b','c','a','a','b']， 可以分成['a', 'b', 'c'], ['a', 'b'], ['a']
['a', 'a', 'a', 'b', 'b', 'b']，可以分成['a', 'b'], ['a', 'b'], ['a', 'b']

## Approach 1
Use a Hashmap to keep a record of the occurence of each character. If one character occurs `k` times, then it should be added to the `k+1` list. If there is only `k` lists, then a new list should be created.

```java
class Solution {
    public List<List<Character>> splitCharacter(char[] strs){
        Map<Character, Integer> map = new HashMap<>();
        List<List<Character>> result = new ArrayList<>();
        
        for (int i = 0; i < strs.length; i++) {
            char c = strs[i];
            int k = map.getOrDefault(c, 0);
            //if occurence == number of lists, create a new list
            if (k == result.size())
                result.add(new ArrayList<Character>());
            //add it to the 
            result.get(k).add(c);
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        return result;
    }
}
```

## Approach 2
```java
    public List<List<Character>> splitCharacter(char[] strs){
        char[] map = new char[256];
        List<List<Character>> result = new ArrayList<>();
        
        for (int i = 0; i < strs.length; i++) {
            char c = strs[i];
            int k = map[c];
            if (k == result.size())
                result.add(new ArrayList<Character>());
            result.get(k).add(c);
            map[c]++;
        }
        return result;
    }
```