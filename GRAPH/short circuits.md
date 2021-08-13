#  Short Circuits


- _Description_
  Given a list of words words, determine whether the words can be chained to form a circle. A word X can be placed in front of another word Y in a circle if the last character of X is same as the first character of Y. All words must be used and can only be used once (excluding the first/last word).
  Contraints = <code>words ≤ 15000</code>
  
    Input: arr[] = {"for", "geek", "rig", "kaf"}
    Output: Yes, the given strings can be chained.
    The strings can be chained as "for", "rig", "geek" 
    and "kaf"


    Intuition - Euler tour and a bit manipulation with the in degree and out degree to make it work in O(n)

- Solution

```
void DFS(int u, vector<bool>& vis, vector<int> list[]) {
    vis[u] = 1;
    for (int v : list[u]) {
        if (!vis[v]) {
            DFS(v, vis, list);
        }
    }
}
bool solve(vector<string>& words) {
    int n = words.size(), len;
    vector<int> ino(256, 0);
    vector<int> out(256, 0);
    vector<int> list[256];
    vector<bool> vis(256, 0);
    for (int i = 0; i < n; i++) {
        len = words[i].size();
        int u = tolower(words[i][0]) - 'A', v = tolower(words[i][len - 1]) - 'A';
        out[u]++,ino[v]++;
        list[u].push_back(v);
    }
    for (int i = 0; i < 256; i++) {
        if (ino[i] != out[i]) {
            return false;
        }
    }
    int u = tolower(words[0][0]) - 'A';
    DFS(u, vis, list);
    for (int i = 0; i < 256; i++) {
        if (ino[i] > 0 && vis[i] == false) {
            return false;
        }
    }
    return true;
}
```