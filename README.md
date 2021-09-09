# Leetcode-1092


 int dp[1001][1001];
    void lcs(string s1, string s2){
        int x = s1.length();
        int y = s2.length();
        for(int i = 0 ; i <= x ; i++){
            for(int j = 0 ; j <= y ; j++){
                if(i == 0 || j == 0)
                    dp[i][j] = 0;
            }
        }
        for(int i = 1 ; i <= x ; i++){
            for(int j = 1 ; j <= y ; j++){    
                if(s1[i-1] == s2[j-1])
                    dp[i][j] = 1 + dp[i-1][j-1];
                else
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
        //return dp[x][y];
    }
    string shortestCommonSupersequence(string str1, string str2) {
        
        lcs(str1, str2);
        string s = "";
        int i = str1.length();
        int j = str2.length();
        while(i > 0 && j > 0){
            if(str1[i-1] == str2[j-1]){
                s = s + str1[i-1];
                i--;
                j--;
            }
            else if(dp[i-1][j] > dp[i][j-1]){
                s += str1[i-1];
                i--;
            }
            else{
                s += str2[j-1];
                j--;
            }
        }
        while(i > 0){
             s += str1[i-1];
             i--;
        }
        while(j > 0){
               s += str2[j-1];
                j--; 
        }
        reverse(s.begin(),s.end());
        return s;
    }
};
