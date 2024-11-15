### coin change
```
class Solution {
  public:
    int f(vector<int>& coins ,int n , int i , int sum , vector<vector<int>>& dp){
        if(sum == 0) return 1;
        if(sum < 0) return 0;
        if(i >= n) return 0;
        if(dp[i][sum] != -1) return dp[i][sum];
        int ntk = f(coins , n , i + 1 , sum , dp);
        int tk = 0;
        if(sum >= coins[i]){
            tk = f(coins , n , i , sum - coins[i] , dp);
        }
        return  dp[i][sum] =  tk + ntk;
        
    }
    int count(vector<int>& coins, int sum) {
    
        int n = coins.size();
        vector<vector<int>> dp(n+1 , vector<int>(sum+1 , -1));
        return f(coins , n , 0 , sum , dp);
    }
};
T.C -> O(N^2);
S.C -> O(N^2);
```

### first transititon point
```
class Solution {
  public:
    int transitionPoint(vector<int>& arr) {
        int l = 0;
        int r = arr.size();
        
        while((r - l) > 0){
            int m = l + (r - l) / 2;
            if(arr[m] < 1) l = m + 1;
            else r = m;
        }
        if(l < arr.size() && arr[l] == 1) return l;
        return -1;
        
        
    }
};
T.C -> o(logn);
S.c -> o(1);
```

### first repeating element
```
class Solution {
  public:
    int firstRepeated(vector<int> &arr) {
        map<int ,int> mp;
        int mn = INT_MAX;
        for(int i = 0 ; i < arr.size() ; i++){
            if(mp.count(arr[i]) > 0) {
                mn = min(mn , mp[arr[i]]);
            }
            else mp[arr[i]] = i;
        }
        return mn == INT_MAX ? -1 : mn + 1;
    }
};
T.C -> o(n);
S.C -> o(n);
```

### remove duplicates
```
class Solution {
  public:
    int remove_duplicate(vector<int> &arr) {
        int i = 0;
        int n = arr.size();
        int j = 0;
        while(j < n){
            if(arr[j] != arr[i]){
                ++i;
                arr[i] = arr[j];
            }
            j++;
        }
        return i + 1;
        
    }
};
T.C -> o(n);
S.C -> o(1);
```

### wave array
```
class Solution {
  public:
    
    void convertToWave(vector<int>& arr) {
        int n = arr.size();
        int i = 0;
        int j = 1;
        while(i < n && j < n){
            swap(arr[i] , arr[j]);
            i+=2;
            j+=2;
        }
        return;
    }
};
T.C -> o(n);
S.C -> o(1);
```

### first and last occurence
```
class Solution {
  public:
    int lowerbound(vector<int>& arr , int x){
        int l = 0 ;
        int r = arr.size();
        while((r - l) > 0){
            int m = l + (r - l) / 2;
            if(arr[m] < x) l  = m + 1;
            else r = m;
        }
        return l;
    }   
    int upperbound(vector<int>& arr , int x){
        int l = 0 ;
        int r = arr.size();
        while((r - l ) > 0){
            int m = l + (r - l) / 2;
            if(arr[m] <= x) l  = m + 1;
            else r = m;
        }
        return l;
    }
    vector<int> find(vector<int>& arr, int x) {
        int fi = lowerbound(arr , x);
        int se = upperbound(arr , x);
        if(fi < arr.size() && arr[fi] != x) return {-1, -1};
        --se;
        if(se < arr.size() && se >= 0 && arr[se] != x) return {-1 , -1};
        
        return {fi , se};
    }
};

T.C -> o(logn);
S.C -> o(1);
```

### stock buy and sell
```
class Solution{
public:
    vector<vector<int> > stockBuySell(vector<int> A, int n){
        vector<vector<int>> ans;
        for(int i  =0 ; i < n - 1 ; i++){
            if(A[i + 1] - A[i]  > 0) ans.push_back({i , i + 1});
        }
        return ans;
    }
};
T.C -> o(n);
S.C -> o(n);
```