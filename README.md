# Longest Repeating Character Replacement
https://leetcode.com/problems/longest-repeating-character-replacement

You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.
```java
Example 1:

Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.

Example 2:

Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.
``` 

## Constraints:

1. 1 <= s.length <= 10^5
2. s consists of only uppercase English letters.
3. 0 <= k <= s.length

## Implementation 
```java
public class Solution {
    public int characterReplacement(String s, int k) {
        // Frequency array to store the counts of characters in the current window
        int[] count = new int[26];
        int maxLen = 0;       // To store the maximum length of the valid window
        int maxCount = 0;     // To store the count of the most frequent character in the current window
        int left = 0;         // Left pointer for the sliding window
        
        for (int right = 0; right < s.length(); right++) {
            // Update the count of the current character (using 'A' as the base)
            count[s.charAt(right) - 'A']++;
            
            // Update the maxCount of the most frequent character in the window
            maxCount = Math.max(maxCount, count[s.charAt(right) - 'A']);
            
            // If the window becomes invalid (too many replacements), shrink it by moving the left pointer
            int windowLength = right - left + 1;
            int requiredReplacements = windowLength - maxCount;
            if (k < requiredReplacements) {
                count[s.charAt(left) - 'A']--;
                left++;
            }
            
            maxLen = Math.max(maxLen, right - left + 1);
        }
        
        return maxLen;
    }
}
```

