class Solution {
    // Tc: O(N×L+26^M)
    class Trie {
        boolean isEnd;
        Trie[] children;

        public Trie() {
            this.children = new Trie[26];
        }
    }

    Trie root;

    public void insert(String word) {
        Trie curr = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            if (curr.children[ch - 'a'] == null) {
                curr.children[ch - 'a'] = new Trie();
            }
            curr = curr.children[ch - 'a'];
        }
        curr.isEnd = true;
    }

    StringBuilder ans;

    public String longestWord(String[] words) {
        root = new Trie();
        ans = new StringBuilder();
        for (String word : words) {
            insert(word);
        }
        backtrack(root, new StringBuilder());
        return ans.toString();

    }

    private void backtrack(Trie curr, StringBuilder curStr) {

        if (curStr.length() > ans.length()) {
            ans = new StringBuilder(curStr);
        }

        for (int i = 0; i < 26; i++) {
            if (curr.children[i] != null && curr.children[i].isEnd) {
                int le = curStr.length();
                curStr.append((char) (i + 'a'));
                backtrack(curr.children[i], curStr);
                curStr.setLength(le);
            }
        }
    }
}