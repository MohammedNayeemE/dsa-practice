### 3-sum-closest
```
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int ans = INT_MAX / 2;
        int n = nums.size();
        int S = 0;
        sort(nums.begin() , nums.end());
        for(int i= 0  ; i < n - 2 ; ++i) {
            int l = i + 1;
            int r  = n - 1;
            int X = nums[i];
            while((r - l) > 0) {
                S = X + nums[l] + nums[r];
                if(abs(S - target) < abs(ans - target)) ans = S;
                if(S == target) return S;
                if(S > target) r--;
                if(S < target) l++; 
            }
        }
        return ans;

    }
};
T.C -> o(n^2);
S.C -> o(1);
```

### jump-game 2
```
class Solution {
public:
    int f(int i , vector<int>& nums ,int n , vector<int>& dp) {
        if(i >= n - 1) return 0;
        if(dp[i] != -1) return dp[i];
        int ans = INT_MAX;
        for(int j = 1 ; j <= nums[i] ; j++) {
            int l = f(i + j , nums , n , dp);
            if(l != INT_MAX) ans = min(ans , 1 + l);
        }
        return dp[i] = ans;

    }
    int jump(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n ,-1);
        return f(0 , nums , n , dp);
    }
};
T.C -> o(n^max(nums));
S.C -> o(n);
```

### group-anagrams
```
class Solution {
public:
    #define se second
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        map<string , vector<string>> mp;
        for(auto it : strs){
            string s = it;
            sort(s.begin() , s.end());
            if(mp.count(s) == 0) {
                mp[s] = {};
            }
            mp[s].push_back(it);
        }
        vector<vector<string>> ans;
        for(auto& it : mp) {
            vector<string> t;
            for(auto ji  : it.se) t.push_back(ji);
            ans.push_back(t);
        }
        return ans;
    }
};
T.C -> o(n^2logn + n^2) ~= o(n^2logn);
S.C -> o(n^2);
```

### buy and sell stock 2
```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int S = 0;
        int n = prices.size();
        for(int i = 0 ; i < n - 1 ; i++) {
            if(prices[i] < prices[i+1]) S += abs(prices[i] - prices[i+1]);
        }
        return S;
    }
};
T.C -> o(n);
S.C -> o(1);
```

### decode-ways
```
class Solution {
public:
    #define fi first
    #define se second
    int dp[101];
    int f(int i , int n , string& s , map<string , string>& mp) {
        if(i >= n) return 1;
        if(dp[i] != -1) return dp[i];
        int one = 0;
        int two = 0;
        if(mp.count(string(1 , s[i])) > 0) one = f(i + 1 , n , s , mp);
        if(i + 1 < n) {
            string t ;
            t += s[i];
            t += s[i+1];
            if(mp.count(t) > 0) two = f(i + 2 , n  , s , mp);
        }
        return  dp[i] = one + two;
    }
    int numDecodings(string s) {
        int n = s.size();
        map<string , string> mp;
        memset(dp , -1 , sizeof(dp));
        char x = 'A';
        for(int i = 1 ; i <= 26 ; i++) {
            string a = to_string(i);
            mp[a] = string(1 , x);
            x++;
        } 
        return f(0 , n , s , mp);
    }
};

T.C -> o(n);
S.C -> o(n);

```