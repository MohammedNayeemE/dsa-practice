### next-permutation
```
class Solution {
public:
 void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int ind = -1;
        for(int i = n - 2 ; i >= 0 ; i--) {
            if(nums[i] < nums[i + 1]) {
                ind = i;
                break;
            }
        }
        if(ind == -1) {
            reverse(nums.begin() , nums.end());
            return;
        }
        int ind2 = -1;
        for(int i = n - 1 ; i >= ind ; i--) {
            if(nums[i] > nums[ind]) {
                ind2 = i;
                break;
            }
        }
        swap(nums[ind] , nums[ind2]);
        reverse(nums.begin() + ind + 1 , nums.end());
        return;
        
    }
};
T.C -> o(n);
S.C -> o(1);
```

### spiral matrix
```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        int top = 0;
        int left = 0;
        int right = n - 1;
        int btm = m - 1;
        vector<int> ans;
        while (top <= btm && left <= right) {
            for (int i = left; i <= right; i++) {
                ans.push_back(matrix[top][i]);
            }
            top++;
            for (int i = top; i <= btm; i++) {
                ans.push_back(matrix[i][right]);
            }
            right--;
            if (top <= btm) {
                for (int i = right; i >= left; i--) {
                    ans.push_back(matrix[btm][i]);
                }
            }
            btm--;
            if (left <= right) {
                for (int i = btm; i >= top; i--) {
                    ans.push_back(matrix[i][left]);
                }
            }
            left++;
        }
        return ans;
    }
};

T.C -> o(n^2);
S.c -> o(1);

```

### longest substring without repeating characeters
```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> f(26 , -1);
        int n = s.size();
        int i = 0;
        int mx = 0;
        for(int j  =0 ; j < n ; j++) {
            if(f[s[j] - 'a'] != -1 && f[s[j] - 'a'] >= i) {
                i = f[s[j] - 'a'] + 1;
            }
            f[s[j] - 'a'] = j;
            mx = max(mx , j - i + 1);
        }
        return mx;
    }
};

T.C -> o(n);
S.C -> o(26) ~= o(1);

```

### remove linked list elements
```
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if(!head) return nullptr;
        vector<int> ans;
        ListNode* curr = head;
        while(curr != nullptr) {
            if(curr-> val != val) ans.push_back(curr->val);
            curr = curr->next;
        }
        ListNode* dummyNode = new ListNode(0);
        ListNode* scurr = dummyNode;
        for(auto it : ans) {
            ListNode* new_node = new ListNode(it);
            scurr->next = new_node;
            scurr = scurr-> next;
        }
        return dummyNode->next;
    }
};
T.C -> o(n);
S.C -> o(n);
```

### palindrome linked list
```
class Solution {
public:
    ListNode* find_middle(ListNode* head){
        ListNode* slow  = head;
        ListNode* fast = head;
        while(fast != nullptr && fast->next != nullptr) {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
    ListNode* reverse(ListNode* head){
        ListNode* curr = head;
        ListNode* prev = nullptr;
        while(curr != nullptr){
            ListNode* next = curr->next;
            curr->next = prev;
            prev =  curr;
            curr = next;
        }
        return prev;
    }
    bool isPalindrome(ListNode* head) {
        ListNode* middle = find_middle(head);
        ListNode* rhead  = reverse(middle); 
        ListNode* f = head;
        ListNode* s = rhead;
        while(f != middle && s != nullptr) {
            if(f->val != s->val) return false;
            f = f->next;
            s = s->next;
        }
        return true;
    }
};

T.C -> o(n);
S.C -> o(n);
```

### minimum path sum
```
class Solution {
public:
    #define fi first
    #define se second
    vector<pair<int , int>> _dir = {{ 0 , 1} , {1 , 0}};
    int f(vector<vector<int>>& grid , pair<int , int>& src , pair<int , int>& des){
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<int>> dist(m , vector<int>(n , INT_MAX));
        dist[src.fi][src.se] = grid[0][0];
        priority_queue<pair<int , pair<int , int>> , vector<pair<int , pair<int , int>>> , greater<pair<int ,pair<int, int>>>> minH;
        minH.push({grid[0][0] , {0 , 0}});

        while(!minH.empty()) {
            int i = minH.top().se.fi;
            int j = minH.top().se.se;
            int wt = minH.top().fi;
            minH.pop();
            if(i == m - 1 && j == n - 1) break;
            for(auto it : _dir) {
                int di = it.fi + i;
                int dj = it.se + j;
                if(di >=0 && di < m && dj >=0 && dj < n) {
                    if(dist[di][dj] > wt + grid[di][dj]) {
                        dist[di][dj] = wt + grid[di][dj];
                        minH.push({dist[di][dj] , {di , dj}});
                    }
                }
            }
        }
        return dist[des.fi][des.se];
    }
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        pair<int , int> src = {0 , 0};
        pair<int ,int>  des = {m -1 , n -1};
        return f(grid , src , des);
        
    }
};
T.C -> o(n^2logn);
S.C -> o(n^2);
```

### validate binary search tree
```
class Solution {
public:
    bool dfs(TreeNode* root , long long min , long long max) {
        if(!root) return true;
        if(root->val >= max || root->val <= min) return false;
        return dfs(root->left , min , root->val) && dfs(root->right , root->val , max);
    }
    bool isValidBST(TreeNode* root) {

        return dfs(root , LLONG_MIN , LLONG_MAX);
    }
};
T.C -> o(n);
S.C -> o(n);
```

### course-schedule
```
class Solution {
public:
    int kahns(vector<vector<int>>& adj , int N){
        queue<int> q;
        vector<int> indeg(N , 0);
        for(int i = 0 ; i < N ; i++) {
            for(auto it : adj[i]) {
                indeg[it]++;
            }
        }
        for(int i = 0 ; i < N ; i++) { if(indeg[i] == 0) q.push(i);}
        vector<int> ans;
        while(!q.empty()) {
            int node = q.front();
            q.pop();
            ans.push_back(node);
            for(auto it : adj[node]){
                indeg[it]--;
                if(indeg[it] == 0) q.push(it);
            }
        } 
        return ans.size() == N;
    }
    bool canFinish(int numCourses, vector<vector<int>>& edges) {
        int N = numCourses;
        vector<vector<int>> adj(N);
        int m = edges.size();
        for(int i = 0 ; i < m ; ++i) {
            int u = edges[i][0];
            int v = edges[i][1];
            adj[u].push_back(v);
        }
        return kahns(adj , N);
    }
};
T.C -> o( N + m);
S.C -> o(N);
```

### word ladder
```
class Solution {
public:
    int ladderLength(string src, string dest, vector<string>& wordList) {
        unordered_set<string> st;
        for(auto it : wordList) st.insert(it);
        auto bfs = [&]() -> int {
            queue<pair<string , int>> q;
            q.push({src , 1});
            unordered_set<string> visit;

            while(!q.empty()) {
                auto [node , steps] = q.front();
                q.pop();
                if(node == dest) return steps;
                visit.insert(node); 
                for(int i = 0; i < node.size(); ++i) {
                    char y = node[i];
                    for(char x = 'a'; x <= 'z'; x++) {
                        if(x != y) {  
                            node[i] = x;
                            if(visit.find(node) == visit.end() && st.find(node) != st.end()) {
                                visit.insert(node);
                                q.push({node, steps + 1});
                            }
                        }
                    }
                    node[i] = y;  
                }
            }

            return 0; 
        };

        return bfs();
    }
};

T.C -> o(N * word.length * 26);
S.C -> o(N);

```

