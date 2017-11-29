# Knuth Optimization - DP  

Knuth Optimization은 Dynamic Programming에서 점화식이 특정 조건을 만족할 때 활용할 수 있는 최적화 기법이다.

조건 1 DP 점화식 꼴  
*(i<k<j) 일 때,* ``D[i][j] = min(D[i][k] + D[k][j]) + C[i][j]``

조건 2 Quadrangle Inequalty (사각부등식)  
``C[a][c] + C[b][d] ≤ C[a][d] + C[b][c], a ≤ b ≤ c ≤ d``

조건 3 Monotonicity (단조성)  
``C[b][c] ≤ C[a][d], a ≤ b ≤ c ≤ d``  

조건 2와 조건 3을 만족하면 ``A[i][j] = D[i][j]``가 최소가 되기 위한 가장 작은 k라고 했을 때 아래 식을 만족한다.  
``A[i][j−1] ≤ A[i][j] ≤ A[i+1][j]``

위 부등식을 통해 원래 O(N3)O(N3)으로 해결되는 것이 O(N2)O(N2)에 해결된다.

**참고 : [11066번 파일합치기](https://github.com/dohun94/algorithm/blob/master/src/%EB%B0%B1%EC%A4%80/%EB%8F%99%EC%A0%81%EA%B3%84%ED%9A%8D%EB%B2%95/FileConquer.java)**
**출처 : http://blog.myungwoo.kr/98 [PS 이야기]**
