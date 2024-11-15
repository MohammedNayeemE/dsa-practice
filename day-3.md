### kth smallest element

```
class Solution {
  public:
    int kthSmallest(vector<int> &arr, int k) {
        priority_queue<int> maxH;
        for(auto it : arr){
            maxH.push(it);
            if(maxH.size() > k) maxH.pop();
        }
        return maxH.top();
    }
};

T.C -> O(NLOGK)
S.C -> O(N)

```

### minimise heights

```
class Solution {  
  public:  
    int getMinDiff(vector<int> &arr, int k) {  
        int n =arr.size();  
        sort(arr.begin(),arr.end());  
        int mini =0;  
        int maxi =0;  
        int min_diff= arr[n - 1] - arr[0];  
        for(int i =1;i< n;i++){  
            if(arr[i] < k)  
                continue;  
                  
                mini = min(arr[0] + k,arr[i] - k);  
                maxi = max(arr[n - 1] - k,arr[i -1] + k);  
                  
                min_diff = min(min_diff,maxi - mini);  
        }  
        return min_diff;  
    }  
};

T.C -> o(nlogn);
S.C -> o(1);

```

### paranthesis checker
```
class Solution {
  public:
    bool isParenthesisBalanced(string& s) {
        stack<char> st;
        for(char x : s){
            if(x == '(' || x == '{' || x == '['){
                st.push(x);
            }
            else if(!st.empty()){
                if(x == ')' && st.top() == '(') st.pop();
                else if(x == '}' && st.top() == '{') st.pop();
                else if(x == ']' && st.top() == '[') st.pop();
                else return false;
            }
            else return false;
        }
        return st.empty();
    }
};
T.C -> O(N);
S.C -> O(N);
```

### equlibrium point

```
class Solution {
  public:  
    int equilibriumPoint(vector<int> &arr) {
        int n = arr.size();
        vector<int> p(n , 0);
        vector<int> s(n , 0);
        p[0] = arr[0];
        s[n-1] = arr[n-1];
        for(int i = 1 ; i < n ; i++){
            p[i] = p[i-1] + arr[i];
        }
        for(int i = n - 2 ; i >= 0 ; i--){
            s[i] = s[i+1] + arr[i];
        }
        
        for(int i = 0 ; i < n ; i++){
            int left = p[i] - arr[i];
            int right = s[i] - arr[i];
            if(left == right) return i + 1;
        }
        return -1;
    }
};
T.C -> O(N);
S.C -> O(N);
```

### binary search
```
class Solution {
  public:
    typedef long long ll;
    ll bs(ll low, ll high, function<bool(ll)> f) {
        for (ll diff = high - low; diff > 0; diff /= 2) {
            while (low + diff < high && f(low + diff)) low += diff;
        }
        return low;
    }
    
    int binarysearch(vector<int> &arr, int k) {
        ll i = bs(-1, arr.size(), [&](ll mid) {
            return arr[mid] < k;
        });
        ++i;
        return (i < arr.size() && arr[i] == k) ? i : -1;
    }
};
T.C -> O(LOGN)
S.C -> O(1)
```

### Next Greater Element
```
class Solution {
  public:
    vector<int> nextLargerElement(vector<int>& arr) {
        int n = arr.size();
        vector<int> ans(n , -1);
        stack<int> st;
        for(int i = n-1 ; i >=0 ; i--) {
            while(!st.empty() && arr[i] >= st.top()) st.pop();
            if(st.empty()) ans[i] =-1;
            else ans[i] = st.top();
            
            st.push(arr[i]);
        }
        return ans;
    }
};
T.C -> o(n);
S.C -> o(n);
```

### union of two sorted arrays
```
class Solution {
  public:
    int findUnion(vector<int>& a, vector<int>& b) {
        set<int> st;
        for(auto it : a) st.insert(it);
        for(auto it : b) st.insert(it);
        return st.size();
    }
};
T.C -> o(n);
S.C -> o(n);
```
