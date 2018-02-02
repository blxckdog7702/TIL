# 최장 공통 부분 수열(longest common subsequence)  

![lcs](image/lcs.svg)  

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

### 두 문자열간 diff 출력하기  
dp배열의 오른쪽 아래부터 왼쪽 위로 올라간다. x,y가 같다면 왼쪽 위로 이동하고, x,y가 다르다면 왼쪽과 위쪽 중 큰 수로 이동한다. 만약 왼쪽과 위쪽이 같다면 위쪽으로 이동하게 된다. 왼쪽과 위쪽이 같을 때 왼쪽으로 이동하면 결과가 다르게 나온다.  
```  
int backX = longStr.length();
int backY = shortStr.length();

while(backX > 0 && backY > 0) {
  if(shortStr.charAt(backY - 1) == longStr.charAt(backX - 1)) {
    sb.append(shortStr.charAt(backY - 1));
    backX--;
    backY--;
    } else {
      //이 부분 >=를 >로 바꾸면 다른 결과가 나온다.
      if(dp[backY - 1][backX] >= dp[backY][backX - 1]) {
        backY--;
        } else {
          backX--;
        }
    }
}
```  
