## Prolem setting
给了三个String A， B， C，把String A里面所有的B都换成C，然后输出一个新的String

## Solution
class Solution {
    public String replace(String A, String B, String C) {
        int i = 0;
        StringBuilder sb = new StringBuilder();
        while (i < A.length()) {
            int t = 0;
            int j = i;
            //compare A[j] with B[t]
            while (j < A.length() && t < B.length() && A.charAt(j) == B.charAt(t)) {
                j++;
                t++;
            }
            //A[i, j) == B, match!
            if (t == B.length()) {
                sb.append(C);
                i = i + B.length();
            }
            //didn't match
            else {
                sb.append(A.charAt(i));
                i++;
            }
        }
        return sb.toString();
    }
}

## Another problem (Indeed)
题目是：“all” ，“There is all in all, two all”
输出：“There is <b>all</b> in <b>all</b>, two all”;

## Solution
Set B = "all", C = "<b>all</b>"
