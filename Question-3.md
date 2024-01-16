# Câu 3: Thu mua nông sản
Tóm tắt bài toán: 
- Cho 1 cây có $N$ đỉnh, mỗi đỉnh $u$ có màu $A[u]$ thuộc một trong $K$ màu, mỗi màu $i$ có một hệ số $C[i]$ cho trước.
Với một cặp đỉnh $(u, v)$, gọi $W[i]$ là số đỉnh có màu $i$ nằm trên đường đi từ $u$ đến $v$.
Định nghĩa $cost(u, v) = C[1] × W[1]^2 + C[2] × W[2]^2 + … + C[K] × W[K]^2$.
- Có $Q$ truy vấn, truy vấn thứ $j$ cập nhật màu của đỉnh $T[j]$ thành $B[j]$.
Lúc ban đầu và sau mỗi truy vấn thứ $j$, ta cần tính $ans[j]$ là tổng các $cost(u, v)$ với $1 ≤ u < v ≤ N$, lấy dư với 998244353 (Quy ước $ans[0]$ là đáp án lúc ban đầu).
## Phân tích ràng buộc bài toán:
- $1 \le N,Q \le 2 \times {10^5},1 \le K \le 20,1 \le C\left[ i \right] \le {10^9}$
- Ta có bảng biểu diễn chi tiết như sau:

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/7c6583e3-f0d4-425a-8788-cb3a68258786)

## Phân tích từng Subtask: 
### Subtask 1 (7.5%): $N ≤ 30, Q ≤ 800$
- Ở mỗi truy vấn, đầu tiên ta duyệt qua mọi đỉnh $u$, sau đấy chạy DFS bắt đầu từ $u$ và đồng thời cập nhật $W$.
Cụ thể hơn, khi đi vào đỉnh $v$, ta sẽ tăng $W[a[v]]$ lên 1, còn khi đi ra đỉnh $v$ thì sẽ giảm $W[a[v]]$ đi 1. Ngoài ra, nếu $u < v$ thì ta sẽ tăng đáp án lên tổng của $C[i] × W[i]^2$ với mọi $i$.
- Độ phức tạp: $O(Q × N^2K)$.
```cpp
int W[maxK];
int ans;

void add_cost_to_ans(){
    for (int i = 1; i <= K; i++){
        ans += (long long)C[i] * (W[i] * W[i]) % mod;
        if (ans >= mod) ans -= mod;
    }
}

void dfs(int u, int p = -1){
    W[A[u]]++;
    for (auto v: adj[u]){
        if (v == p) continue;
        if (u < v) add_cost_to_ans();
        dfs(v, u);
    }
    W[A[u]]--;
}

void query(){
    ...
    ans = 0;
    for (int u = 1; u <= N; u++){
        dfs(u);
    }
    cout << ans << "\n";
}
```
### Subtask 2 (12.5%): $N ≤ 100, Q ≤ 800$
- Ta có thể cải thiện thuật toán ở subtask 1 bằng việc nhận xét rằng: Ở mỗi bước DFS, để ý rằng ta chỉ thay đổi đúng một giá trị $W[i]$ duy nhất. Do vậy, ta có thể cập nhật tổng của $C[i] × W[i]^2$ trong $O(1)$ trong lúc đang DFS luôn.
- Độ phức tạp: $O(Q × N^2)$.
```cpp
void dfs(int u, int p = -1, int tans = 0){
    tans -= (long long)C[i] * (W[i] * W[i]) % mod;
    if (tans < 0) tans += mod;
    W[A[u]]++;
    tans += (long long)C[i] * (W[i] * W[i]) % mod;
    if (tans >= mod) tans -= mod;
    for (auto v: adj[u]){
        if (v == p) continue;
        if (u < v){
            ans += tans;
            if (ans >= mod) ans -= mod;
        }
        dfs(v, u, tans);
    }
    W[A[u]]--;
}
```
### Subtask 3 (10%): $N ≤ 2000, Q ≤ 800$
- Để ý rằng các màu trong hàm $cost (C[i] × W[i]^2)$ độc lập với nhau, nên ta sẽ xử lí từng màu riêng biệt. Cụ thể hơn, gọi $cost_{i}(u, v) = W[i]^2$, khi đó $\sum_{u,v} cost(u, v) = \sum_{i} C[i] × (\sum_{u,v} cost_{i}(u, v))$ với mọi $i$.
- Để tính $\sum_{u,v} cost_{i}(u, v)$, ta sẽ sử dụng quy hoạch động trên cây. Giả sử cây có gốc ở đỉnh 1.
- Gọi $DP[u][j]$ $(0 ≤ j ≤ 2)$ là tổng $W[i]^j$ của mọi cặp đường đi $(u, y)$ nằm trong cây con gốc $u$. Ban đầu cây con $u$ chỉ có đúng đỉnh $u$, sau đó ta sẽ thêm lần lượt các cây con gốc $v$ với $v$ là con trực tiếp của $u$ vào, đồng thời cập nhật giá trị $DP[u][j]$ và $\sum_{u,v} cost_{i}(u, v)$.
- Độ phức tạp: $O(Q × NK)$.
### Subtask 4 (15%): $N ≤ 5000, Q ≤ 8000$
- Để ý rằng với mỗi truy vấn cập nhật màu của đỉnh $T[j]$ thành $B[j]$, chỉ có 2 màu khác nhau mà giá trị $\sum_{u,v} cost_{i}(u, v)$ thay đổi: $A[T[j]]$ cũ và $B[j]$. Vậy ta chỉ cần tính lại giá trị trên với đúng hai màu này thay vì toàn bộ $K$ màu.
- Độ phức tạp: $O(Q × N)$.
```cpp
// Code chưa xử lí modulo

int ans = 0;
int dp[N][3];

void dfs(int i, int u, int p = -1){
    dp[u][0] = 1; dp[u][1] = dp[u][2] = (a[u] == i ? 1 : 0);
    for (auto v: adj[u]){
        if (v == p) continue;
        dfs(i, v, u);
        // Cộng thêm các đường đi đi qua cạnh (u, v) vào đáp án
        ans += dp[u][2] + dp[v][2] * dp[u][1] * dp[v][1];
        // Cộng thêm v vào u
        dp[u][0] += dp[v][0];
        dp[u][1] += dp[v][1];
        dp[u][2] += dp[v][2];
        if (a[u] == i){
            dp[u][1] += dp[v][0];
            dp[u][2] += 2 * dp[v][1] + dp[v][0];
        }
    }
}
```



