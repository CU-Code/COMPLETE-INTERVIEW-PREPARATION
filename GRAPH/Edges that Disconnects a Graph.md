# Edges that Disconnects a Graph

- Description
    You are given an undirected graph represented as an adjacency list, where graph[i] represents node i's neighbors.

    Return the number of possible edges that, if removed, causes the graph to become disconnected.
- Constraints
<li><code>0 ≤&nbsp;n, m ≤ 250</code> where <code>n</code> and <code>m</code> are the number of rows and columns in <code>graph</code>.</li>

<div class="ExampleTestCases_testcase-content__zYLLV"><div class="ExampleTestCases_testcase__2LeOK"><div class="ExampleTestCases_header___ersR"><h3>Example 1</h3><div class="CopyToTestcaseIcon_copy__izIHo"><div><svg width="18px" height="18px" fill="none" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" preserveAspectRatio="xMidYMid meet"><path d="M5 6.532c0-1.554 1.696-2.514 3.029-1.715l9.113 5.468c1.294.777 1.294 2.653 0 3.43l-9.113 5.468c-1.333.8-3.029-.16-3.029-1.715V6.532z" stroke="#2D2A26" stroke-width="2"></path></svg></div></div></div><div class="ExampleTestCases_title__2pG-e"><h4 class="ExampleTestCases_input__38ARi"><strong>Input</strong></h4><div class=""><div class="VisualizerToggle_toggle__1rVj8"><label>Visualize</label><div class="bs-toggle small"><div class="react-toggle"><div class="react-toggle-track"><div class="react-toggle-track-check"></div><div class="react-toggle-track-x"></div></div><div class="react-toggle-thumb"></div><input class="react-toggle-screenreader-only" type="checkbox" checked=""></div></div></div></div></div><div class="ExampleTestCases_block__3XHen ExampleTestCases_visualizer__t0Ao1"><div class="InputOutputBlock_container__MMlPk"><div class="InputOutputBlock_body__10-4H"><pre>graph = [
    [1, 2, 3, 5],
    [0],
    [0, 3],
    [0, 2, 4],
    [3],
    [0]
]</pre></div></div></div><div class="ExampleTestCases_title__2pG-e"><h4><strong>Output</strong></h4></div><div class="ExampleTestCases_block__3XHen"><div class="InputOutputBlock_container__MMlPk"><div class="InputOutputBlock_body__10-4H InputOutputBlock_output__3E8I8"><pre>3</pre></div></div></div><div class="ExampleTestCases_title__2pG-e"><h4><strong>Explanation</strong></h4></div><div class="ExampleTestCases_explanation__2F8rE"><div class="MarkdownDiv_markdown-div__2auQ4 lightcode"><p>The bridges are <code>[0, 5]</code>, <code>[0, 1]</code>, and <code>[3, 4]</code>.</p>
</div></div></div></div>


- Intuition: Bridges in a graph

- Solution

```
void dfs(int cur, int par,vector<vector<int>>& gr,int &count,vector<int>& low,vector<int>& disc) {
	static int tme=0;
	disc[cur] = low[cur] = tme++;
	for (auto x : gr[cur]) {
		if (disc[x]==-1) {
			dfs(x, cur,gr,count,low,disc);
			// we know low and disc of x
			low[cur] = min(low[cur], low[x]);
			// bridges
			if (low[x] > disc[cur]) {
				count++;
			}
		}
		else if (x != par) {
			// backedge
			low[cur] = min(low[cur], disc[x]);
		}
	}
}

int solve(vector<vector<int>>& graph) {
	int n = graph.size();
	vector<int> low(n,-1),disc(n,-1);
	int count=0;
    dfs(0,-1,graph,count,low,disc);
    return count;
}
```