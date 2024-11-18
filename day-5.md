
### bubble sort
```
  public:
    void bubbleSort(vector<int>& arr) {
        int n = arr.size();
        for(int i = 0 ; i < n - 1 ; i++) {
            for(int j = i + 1 ; j < n ; j++) {
                if(arr[j] < arr[i]) swap(arr[i] , arr[j]);
            }
        }
        return;
    }
};

T.C -> o(n^2);
S.C -> o(1);
```

### non-repeating-character
```
class Solution {
  public:
    char nonRepeatingChar(string &s) {
        int f[26];
        memset(f , 0 , sizeof(f));
        for(auto it : s) f[it - 'a']++;
        for(int i = 0 ; i < s.size() ; i++) {
            if(f[s[i] - 'a'] == 1) return s[i];
        }
        return '$';
    }
};
T.C -> o(n);
S.C -> o(26) ~= o(1);
```

### edit-distance
```
 public:
    int editDistance(string s1, string s2) {
        int m = s1.size();
        int n = s2.size();
        vector<vector<int>> dp(m + 1 , vector<int>(n + 1 , 0));
        for(int i = 0 ; i <= m ; i++) dp[i][0] = i;
        for(int j  =0 ; j <= n ; j++) dp[0][j] = j;
        for(int i = 1 ; i <= m ; i++) {
            for(int j = 1 ; j <= n ; j++) {
                if(s1[i-1] == s2[j-1]) {
                    dp[i][j] = dp[i-1][j-1];
                }
                else{
                    int insert = dp[i][j-1];
                    int _delete = dp[i-1][j];
                    int replace = dp[i-1][j-1];
                    dp[i][j] = 1 + min({insert , _delete , replace});
                }
            }
        }
        return dp[m][n];
    }
};
T.C -> o(n^2);
S.C -> o(n^2);
```

### kth largest elements
```
class Solution {
  public:
    vector<int> kLargest(vector<int>& arr, int k) {
        vector<int> ans(k);
        int l = 0;
        int n = arr.size();
        priority_queue<int ,vector<int>  , greater<int>> minH;
        for(int i = 0 ; i < n ; i++) {
            minH.push(arr[i]);
            if(minH.size() > k) minH.pop();
        }
        while(!minH.empty()) { ans[l++] = minH.top() ; minH.pop() ; }
        reverse(ans.begin() , ans.end());
        return ans;
        
    }
};
T.C -> o(nlogk);
S.C -> o(k);
```

### form the largest number
```
class Solution {
  public:
    string printLargest(vector<int> &arr) {
        sort(arr.begin() , arr.end() , [](auto a , auto b){
           string A = to_string(a);
           string B = to_string(b);
           return A + B >= B + A;
        });
        string ans;
        for(auto it : arr) ans += to_string(it);
        return ans;
        
    }
};
T.C -> o(nlogn);
S.C -> o(n);
```

### quick sort
```
class Solution {
  public:
    void quickSort(vector<int>& arr, int low, int high) {
        if(low < high) {
            int p = partition(arr , low , high);
            quickSort(arr , low , p - 1);
            quickSort(arr , p + 1 , high);
        }
    }
  public:
    int partition(vector<int>& arr, int low, int high) {
        int pivot = arr[low];
        int i = low;
        int j = high;
        while(i < j) {
            while((arr[i] <= pivot) && (i < high)) i++;
            while((arr[j] > pivot) && (j > low)) j--;
            
            if(i < j) swap(arr[i] , arr[j]);
        }
        swap(arr[low] , arr[j]);
        return j;
    }
};

T.C -> o(n^2);
S.C -> o(n);
```