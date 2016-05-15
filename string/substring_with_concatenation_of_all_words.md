# Substring with Concatenation of All Words
## 问题描述
You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

For example, given:
s: "barfoothefoobarman"
words: ["foo", "bar"]

You should return the indices: [0,9].
(order does not matter).
## 分析
设置一个words.length * wordLen长度的滑动窗口，将窗口从左向右滑动，并将窗口再划分为长度为wordlen的块，依次检查每个块是否包含在words中，并且出现次数也是符合要求的。
## 代码实现
```java
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> result = new LinkedList<>();
        if (s.length() == 0 || words.length == 0) return result;
        Map<String, Integer> wordCount = new HashMap<>();
        for (String word : words) {
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }
        int wordLen = words[0].length();
        int winSize = words.length * wordLen;
        for (int i = 0; i <= s.length() - winSize; i++) {
            Map<String, Integer> unused = new HashMap<>(wordCount);
            for (int j = 0; j < winSize; j+=wordLen) {
                String str = s.substring(i + j, i + j + wordLen);
                int count = unused.getOrDefault(str, -1);
                if (count == 1) {
                    unused.remove(str);
                } else if (count > 1) {
                    unused.put(str, count - 1);
                } else {
                    break;
                }


            }
            if (unused.size() == 0) result.add(i);
        }
        return result;
    }
```