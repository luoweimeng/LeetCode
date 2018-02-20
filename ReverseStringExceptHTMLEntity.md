## Problem setting
Reverse string except for HTML entities, i.e, A HTML entities must be treated as an entire word without reverse.

```
e.g. "1234&euro;" => "&euro;4321"
"1234&euro" => "orue&4321"
"1234&euro;567" => "765&euro;4321"
```

## Approach 1

```java
class Solution {
    public String reverseString(String s) {
        char[] ca = s.toCharArray();
        List<String> words = new ArrayList<>();
        int i = 0;
        int j = 0;
        while (j < s.length()) {
            char c = s.charAt(j);
            if (c != '&') {
                j++;
            }
            //c == '&'
            else {
                //'&' is not the first character, reverse the s[i, j), and add it to tokens
                //Add 
                if (j != 0) {
                    String word = reverse(s, i, j - 1);
                    words.add(word);
                }
                
                //Add HTML utity
                StringBuilder sb = new StringBuilder();
                while (j < s.length() && s.charAt(j) != ';') {
                    sb.append(s.charAt(j));
                    j++;
                }
                
                if (j < s.length()) {
                    sb.append(';');
                    words.add(sb.toString());
                    //j point to the first character after ';'
                    j++;
                    i = j;
                }
            }
        }
        
        //reverse the trailing characters
        if (i < j) {
            String word = reverse(s, i, j - 1);
            words.add(word);
        }
        //reverse the tokens
        StringBuilder result = new StringBuilder();
        for (i = words.size() - 1; i >= 0; i--)
            result.append(words.get(i));
        
        return result.toString();
    }
    
    public String reverse(String s, int i, int j) {
        StringBuilder sb = new StringBuilder();
        while (i <= j) {
            sb.append(s.charAt(j));
            j--;
        }
        return sb.toString();
    }
}
```

## Approach 2

A more concise solution, first reverse the whole string, then reverse the HTML entity

```java
//"1234&euro;567" => "765;orue&4321" => "765&euro;4321"
class Solution {
    public String reverseString(String s) {
        List<String> words = new ArrayList<>();
        //reverse the whole string
        s = reverse(s, 0, s.length() - 1);
            
        int i = 0;
        int j;
        while (i < s.length()) {
            //whenever we encounter ";a&" , reverse it
            if (s.charAt(i) == ';') {
                j = i + 1;
                while (s.charAt(j) != '&')
                    j++;
                s = reverse(s, i, j);
                i = j + 1;
            }
            else
                i++;
        }
        return s;
    }
    
    //reverse the string between i and j
    public String reverse(String s, int i, int j) {
        StringBuilder sb = new StringBuilder();
        for (int k = 0; k < s.length(); k++) {
            if (k >= i && k <= j)
                sb.append(s.charAt(i + j - k));
            else
                sb.append(s.charAt(k));
        }
        return sb.toString();
    }
}
```