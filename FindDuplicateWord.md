## Problem setting

Given a words of sentence, e.g. "dog cat fish cat", find out the first duplicated word. In this case, return "cat". .

## Solution

```java
class Solution {
    public String findDuplicate(String strs) {
        String[] words = strs.split(" ");
        Set<String> set = new HashSet<>();
        for (String word : words) {
            if (set.contains(word))
                return word;
            else
                set.add(word);
        }

        return null;
    }
}
```

## Follow up

Instead of returning the first duplicated word, return the earlier duplicated word which has the smallest index. e.g. 
"dog cat fish cat dog" => return dog

```java
class Solution {
    public String findDuplicate(String strs) {
        int minPos = Integer.MAX_VALUE;
        String[] words = strs.split(" ");
        HashMap<String, Integer> map = new HashMap<>();
        for (int i = 0; i < words.length; i++) {
            String word = words[i];
            if (map.containsKey(word)) {
                if (map.get(word) < minPos)
                    minPos = map.get(word);
            }
            else
                map.put(word, i);
        }

        return words[minPos];
    }
}
```