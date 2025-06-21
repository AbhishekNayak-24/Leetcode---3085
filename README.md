# Leetcode---3085
Minimum Deletions to Make String K-Special
//code in java 
import java.util.ArrayList;
import java.util.List;

class Solution {
    private List<Integer> nums = new ArrayList<>();

    public int minimumDeletions(String word, int k) {
        int[] freq = new int[26];
        int n = word.length();
        for (int i = 0; i < n; ++i) {
            ++freq[word.charAt(i) - 'a'];
        }

        for (int v : freq) {
            if (v > 0) {
                nums.add(v);
            }
        }

        int ans = n; // Initialize with the maximum possible deletions (deleting all characters)

        // Iterate through all possible minimum frequencies 'v'
        // The minimum frequency 'v' can range from 0 to the maximum frequency in the original word
        for (int i = 0; i <= n; ++i) { 
            ans = Math.min(ans, f(i, k));
        }
        return ans;
    }

    // Helper function to calculate deletions for a given minimum frequency 'v'
    private int f(int v, int k) {
        int ans = 0;
        for (int x : nums) {
            if (x < v) {
                // If a character's frequency 'x' is less than the target minimum 'v',
                // all 'x' occurrences must be deleted.
                ans += x;
            } else if (x > v + k) {
                // If a character's frequency 'x' is greater than the allowed maximum (v + k),
                // (x - (v + k)) occurrences must be deleted.
                ans += x - (v + k);
            }
        }
        return ans;
    }
}
