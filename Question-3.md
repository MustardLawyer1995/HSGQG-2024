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
### Subtask 7 (15%): Không có điều kiện gì thêm 
- Gọi $sz[u]$ là số đỉnh nằm trong cây con gốc $u$.
- Gọi $contrib(x, y)$ là số lần cặp $(x, y)$ được tính ở $\sum_{u,v} cost_{i}(u, v)$, ta có hai trường hợp:
   - $x$ và $y$ không phải là tổ tiên của nhau, khi đó $contrib(x, y) = sz[x] × sz[y]$.
   - $x$ là tổ tiên của $y$ (trường hợp $y$ là tổ tiên của $x$ tương tự), khi đó $contrib(x, y) = (n - sz[jump(x, y)]) × sz[y]$, với $jump(x, y)$ là con trực tiếp của $x$ mà cũng là tổ tiên của $y$.

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/67e315c7-dd3b-4253-a6aa-5cf7f0824c03)

#### ***Hướng làm 1: Centroid***
   - Để ý trường hợp 2 ($x$ là tổ tiên của $y$) xử lí khó, nên ta sẽ tìm cách biến đổi hết trường hợp 2 về trường hợp 1 bằng centroid.
Nhắc lại tính chất centroid: Mọi đường đi $(x, y)$ đều có thể tách thành 2 đường đi nhỏ hơn $(x, r)$ và $(r, y)$, với $r$ là centroid bé nhất mà cây con centroid gốc $r$ chứa cả $x$ và $y$. Vậy nếu ta để $r$ là gốc của cây thì ta sẽ có thể dùng công thức của trường hợp 1 cho đường đi này.
   - Lưu ý rằng do gốc của cây không cố định, nên ta phải tính hàm $sz(r, u)$ là số đỉnh có màu $i$ nằm trong cây con gốc $u$ với gốc của toàn bộ cây là $r$. Toàn bộ các giá trị này có thể được tính trước trong $O(1)$.
   - Mỗi lần ta cập nhật giá trị của $A[u]$, ta sẽ bò từ $u$ lên các cha centroid $r$ của nó và cập nhật lại tổng của $sz(r, u) × sz(r, v)$ với các đỉnh $v$ khác cũng nằm trong cây con centroid gốc $r$, và không nằm trong cây con centroid gốc $jump(r, u)$. Kĩ thuật này khá cổ điển, xin nhường lại chi tiết cho bạn đọc.
   - Độ phức tạp: $O(N \times log N)$.
#### ***Hướng làm 2: Heavy-Light Decomposition (HLD)***
   - Mỗi lần ta cập nhật giá trị của $A[u]$, ta sẽ xét các trường hợp của đỉnh $v$:
       - $v$ là tổ tiên của $u$: Ta cần tính tổng của $sz[jump(u, v)]$ với mọi $v$. Vì hàm $jump$ rất khó xử lí, ta sẽ biến đổi truy vấn cập nhật đỉnh $u$ thành cập nhật toàn bộ các con của $u$, khi đó truy vấn tính tổng sẽ thành tính tổng các đỉnh từ gốc đến $u$. Để cập nhật toàn bộ các con nhanh, ta sẽ dùng HLD: Ta chỉ cập nhật duy nhất con heavy của $u$ vào cấu trúc dữ liệu. Khi tính tổng, các cạnh heavy đã được cập nhật rồi, còn các cạnh light ta có thể duyệt trâu qua (chỉ có $log N$ cạnh light).
       - Cấu trúc dữ liệu trên cần hỗ trợ truy vấn tính tổng từ đỉnh đến gốc và cập nhật một đỉnh: Fenwick tree trên Euler tour.
       - $u$ là tổ tiên của $v$: Ta sẽ làm đối xứng với trường hợp trước: Chỉ cập nhật các cạnh light và chỉ tính tổng của con heavy.
       - $u$ và $v$ không là tổ tiên của nhau: Nhường làm bài tập cho bạn đọc.
----------------------------------------------------------------------------------------------------------------------------------------
#### ***Nhận xét***: $cost_{i}(u, v)$ bằng với số cặp đỉnh $(x, y)$ có cùng màu $i$ nằm trên đường đi $(u, v)$.

![image](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/fe186c38-c6b7-416f-90c8-4266ec4158fe)

- Ví dụ ở đường đi $u - w$ có 3 đỉnh cùng màu trên, $W[i] = 3, W[i]^2 = 9$, và cũng có 9 cặp đỉnh $(x, y)$ thoả mãn: $(u, u), (u, v), (u, w), (v, u), (v, v), (v, w), (w, u), (w, v), (w, w)$.

- Sử dụng nhận xét này, thay vì tính trực tiếp $\sum_{u,v} cost_{i}(u, v)$, ta có thể đếm xem mỗi cặp đỉnh $(x, y)$ được tính bao nhiêu lần trong tổng trên (kĩ thuật contribution-to-the-sum).
----------------------------------------------------------------------------------------------------------------------------------------

- Độ phức tạp: $O(N \times log N)$.


