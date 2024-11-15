
### floor in sorted array
```
class Solution {
  public:

    int findFloor(vector<int>& arr, int k) {
        int n = arr.size();
        int i = 0 ;
        int j = n;
        while((j - i) > 0) {
            int m = i + (j - i) / 2;
            if(arr[m] < k) i = m + 1 ;
            else j = m;
        }
        if(i < n && arr[i] == k) return i;
        i--;
        if(i >=0 && i < n) return i;
        return -1;
    }
};
T.C -> o(logn)
S.C -> o(1)
```

### check equal arrays
```
#define fi first
#define se second
class Solution {
  public:
    // Function to check if two arrays are equal or not.
    bool check(vector<int>& arr1, vector<int>& arr2) {
        map<int , int> mp;
        for(auto it : arr1) mp[it]++;
        map<int , int> pm;
        for(auto it : arr2) pm[it]++;
        for(auto it = mp.begin() ; it != mp.end() ; it++) {
            if(mp[it->fi] != pm[it->fi]) return false;
        }
        return true;
    }
};
T.C -> o(n)
S.C -> o(n)
```

### palindrome linked list
```
class Solution {
  public:
    Node* reverse(Node* head){
        Node* curr = head;
        Node* prev = NULL;
        
        while(curr != NULL) {
            Node* next = curr->next;
            curr-> next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
    Node* middle(Node* head){
        Node* fast = head;
        Node* slow = head;
        while(fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
    bool isPalindrome(Node *head) {
        Node* middle_node = middle(head);
        Node* reverse_head = reverse(middle_node);
        Node* curr = head;
        Node* scurr = reverse_head;
        while(curr != middle_node && scurr != NULL){
            if(curr->data != scurr->data) return false;
            curr = curr->next;
            scurr = scurr->next;
        }
        return true;
    }
};
T.C -> o(n);
S.C -> o(n);
```

### balaned binary tree
```
struct TreeNode {

int val;

TreeNode *left;

TreeNode *right;

TreeNode() : val(0), left(nullptr), right(nullptr) {}

TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}

TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}

};

class Solution {

public:

int d(TreeNode* root){

if(!root) return 0;

int l = d(root->left);

int r = d(root->right);

return 1 + max(l , r);

}

bool isBalanced(TreeNode* root) {

if(!root) return true;

int left = d(root->left);

int right = d(root->right);

if(abs(left - right) > 1) return false;

return isBalanced(root->left ) && isBalanced(root->right);

}

};
T.C -> o(n^2)
S.C -> o(n)
```

### 3-sum
```
class Solution {
  public:
    bool find3Numbers(int arr[], int n, int x) {
        sort(arr , arr + n);
        for(int i = n - 1 ; i > 0 ; i--){
            int c = arr[i];
            if(c > x) continue;
            int l = 0;
            int r = i-1;
            while(l < r){
                int sum = arr[l] + arr[r] + c;
                if(sum == x) return true;
                else if(sum > x) r--;
                else l++;
            }
        }
        return false;
    }
};

T.C -> o(n^2);
S.C -> o(1);
```

### 0-1 knapsack
```
class Solution {
  public:
    int dp[1001][1001];
    int f(int i , vector<int>& val , vector<int>& wt , int W , int n){
        if(i >= n) return 0;
        if(dp[i][W] != -1) return dp[i][W];
        int ntk = f(i + 1, val , wt , W , n);
        int tk = 0;
        if(W >= wt[i]){
            tk  = val[i] + f(i + 1 , val , wt , W - wt[i] , n);
        }
        return dp[i][W] = max(tk , ntk);
    }
    int knapSack(int capacity, vector<int> &val, vector<int> &wt) {
        memset(dp , -1 , sizeof(dp));
        return f(0 , val , wt , capacity , val.size());
    }
};
T.C -> o(n^2);
S.C -> o(n^2);

```

