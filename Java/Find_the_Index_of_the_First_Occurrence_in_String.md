https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/

#28.Задача на поиск подстроки в строке

1 реализация, универсальный поиск.Сложность О(n*m)

```Java
public static int strStr(String haystack, String needle) {
        if(haystack.length() < needle.length()){
            return -1;
        }
        for (int i = 0; i < haystack.length(); i++) {

            int k = 0;
            while (k < needle.length() && i + k < haystack.length() && haystack.charAt(k+i) == needle.charAt(k)) {
                    k++;
            }
            if(k == needle.length()){
                return i;
            }
        }
        return -1;
    }
```

2 реализация, Алгоритм Кнута-Морриса-Пратта (КМП).Сложность О(n+m)
```Java
  public static int[] findPrefix(String needle) {
        int[] arr = new int[needle.length()];
        for (int i = 1; i < needle.length(); i++) {
            int k = 0;
            while (i + k < needle.length() && needle.charAt(k) == needle.charAt(k+i)) {
                arr[i + k] = Math.max(arr[i + k], k + 1);
                k++;
            }
        }
        return arr;
    }

    public static int strStr(String haystack, String needle) {
        if (haystack.length() < needle.length()) {
            return -1;
        }
        int[] prefix = findPrefix(needle);
        int i = 0;
        int j = 0;
        while (i < haystack.length()) {
            if (haystack.charAt(i) == needle.charAt(j)) {
                i++;
                j++;
            }
            if (j == needle.length()) {
                return i - j;
            } else if (i < haystack.length() && haystack.charAt(i) != needle.charAt(j)) {
                if (j != 0) {
                    j = prefix[j - 1];
                } else i++;
            }
        }
        return -1;
    }
    
```
