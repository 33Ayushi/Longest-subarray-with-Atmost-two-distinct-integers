# Longest-subarray-with-Atmost-two-distinct-integers
Given an array arr[] consisting of positive integers, your task is to find the length of the longest subarray that contains at most two distinct integers.
class Solution {
    public int totalElements(int[] arr) {
        Map<Integer, Integer> freq = new HashMap<>();
        int left = 0, maxLen = 0;

        for (int right = 0; right < arr.length; right++) {
            freq.put(arr[right], freq.getOrDefault(arr[right], 0) + 1);

            // Shrink window if more than 2 distinct
            while (freq.size() > 2) {
                freq.put(arr[left], freq.get(arr[left]) - 1);
                if (freq.get(arr[left]) == 0) {
                    freq.remove(arr[left]);
                }
                left++;
            }

            maxLen = Math.max(maxLen, right - left + 1);
        }

        return maxLen;
    }
}
- Time: O(n) (each element processed at most twice).
- Space: O(2) = O(1) (map holds at most 2 keys).
