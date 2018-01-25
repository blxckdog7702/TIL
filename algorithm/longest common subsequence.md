# 최장 공통 부분 수열(longest common subsequence)  

![lcs](lcs.svg)  

x,y가 비교할 문자열이고, i,j는 그에 해당하는 인덱스라면  
i == 0, j == 0 이면 0  
i == j 면 dp[x][y] = dp[x-1][y-1] + 1;  
i != j 면 dp[x][y] = max(dp[x-1][y], dp[x][y-1]);  

```  
for (int i = 1; i <= shortStr.length(); i++)
  for (int j = 1; j <= longStr.length(); j++)
    if (shortStr.charAt(i - 1) == longStr.charAt(j - 1)) {
      [i][j] = dp[i - 1][j - 1] + 1;
    } else {
      dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
    }
  }
}
```
