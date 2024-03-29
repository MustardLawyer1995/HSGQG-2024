# Câu 5: Mạng truyền tin
- Tóm tắt đề bài: Cho một cây $N$ đỉnh, cạnh thứ $i$ có trọng số là $w_i$. Xét hai đỉnh $u$ và $v$, gọi $P$ là tập hợp các cạnh nằm trên đường đi ngắn nhất từ $u$ đến $v$, ta định nghĩa:
$cost(u, v) = (\text{kích thước của } P) ^ 2 \times (\text{trọng số nhỏ nhất của các cạnh trong } P)$
- Yêu cầu: Với mỗi đỉnh gốc $r$, tính tổng $cost(r, 1) + cost(r, 2) + … + cost(r, N)$ modulo 998244353.
## Phân tích ràng buộc bài toán: 
- $N \le {10^5}$ và trọng số cạnh $\le {10^9}$.
- Khi ấy ta có bảng biểu diễn chi tiết như sau:

| Subtask | Điều kiện  | 
|----------|----------|
| 16% | $N \le 5000$ |
| 12% | $w_{i} \le 2$ và luôn có cạnh giữa $i-1$ và $i$ với mọi $i \ge 2$ |
| 20% | $w_{i}=1$ |
| 16% | $w_{i} \le 1000$ |
| 16% | Luôn có cạnh giữa $i-1$ và $i$ với mọi $i \ge 2$ |
| 20% | Không có ràng buộc gì thêm |

## Phân tích từng Subtask 
### Subtask 1: $N \le 5000$
- Với mỗi gốc $r$, ta dùng thuật toán DFS để tính kết quả.
### Subtask 2: $w_{i} \le 2$ và có cạnh nối $i$ và $i-1$ với mọi $i \ge 2$. 
- Ở subtask này cây có dạng đường thẳng $1 - 2 - … - N$. Để tính kết quả cho đỉnh $i$, nhận thấy rằng $w_{i} \ge 2$, ta sẽ tìm đỉnh $x$ nhỏ nhất sao cho các cạnh từ $x$ đến $i$ đều có trọng số bằng 2. Khi đó:
    - $cost(i, j) = 2 \times {(i - j)^2}$ với $j \ge x$.
    - $cost(i, j) = (i - j)^2$ với $j < x$.
- Các đỉnh $j > i$ ta xét tương tự.
### Subtask 3: $w_{i}=1$
- Lúc này ta không cần quan tâm đến trọng số cạnh nữa. Root cây tại một đỉnh bất kỳ. Gọi $dis(u, v)$ là khoảng cách giữa hai đỉnh $u$ và $v$.
- Ta sẽ tính các mảng sau:
    - $down1[u] =$ tổng $dis(u, v)$ với mọi v nằm trong cây con gốc $u$.
    - $down2[u] =$ tổng $cost(u, v)$ với mọi v nằm trong cây con gốc $u$.
    - $up1[u] =$ tổng $dis(u, v)$ với mọi v nằm ngoài cây con gốc $u$.
    - $up2[u] =$ tổng $cost(u, v)$ với mọi v nằm ngoài cây con gốc $u$.
    - $sz[u] =$ số đỉnh nằm trong cây con gốc $u$.
- Ta tính mảng $down1, down2, sz$ bằng một lượt DFS và $up2, down2$ bằng một lượt DFS khác. Việc tính toán chi tiết xin dành cho bạn đọc.
### Subtask 4,5,6:
- Ta sẽ sử dụng thuật toán phân tách trọng tâm.
- Gọi $ans[u]$ là đáp án cần tính của đỉnh $u$.
- Gọi trọng tâm của cây là đỉnh $c$ và các đỉnh kề với $c$ là $u_{1}, u_{2}, …, u_{k}$. Ta sẽ tính đóng góp của các đường đi qua $c$ vào đáp án của các đỉnh.
- Ta sử dụng DFS để tính $d[v] = dis(c, v)$ và $mn[v]$ là cạnh nhỏ nhất nằm trên đường đi từ $c$ đến $v$ với mọi đỉnh $v$ nằm trong cây hiện tại.
  
![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/9f0676e9-e707-4a5f-a286-a444bc88a4d9)

- Ta sort các pair $(mn[v], d[v])$ theo thứ tự tăng dần của $mn$ (với $v = c$ ta coi như $mn[v] = \infty \$).
- Khi đó: $cost(v_{i}, v_{j}) = (d[v_{i}] + d[v_{j}])^2 \times mn[v_{i}]
                                  = (d[v_{i}] ^ 2 + d[v_{j}] ^ 2 + 2 \times d[v_{i}] \times d[v_{j}]) \times mn[v_{i}]$

- $ans[v_{i}]$ sẽ được cộng lên một lượng:
    - Xét các $j < i$: $\sum(d[v_{j}]^2 \times mn[v_{j}]) + d[v_{i}]^2 \times \sum mn[v_{j}] + 2 \times d[v_{i}] \times \sum (d[v_{j}] \times mn[v_{j}])$
    - Xét các $j > i$: $mn[v_{j}] \times \sum (d[v_{j}]^2) + d[v_{i}]^2 \times mn[v_{i}] \times (n - i) + 2 \times d[v_{i}] \times mn[v_{i}] \times \sum (d[v_{j}])$
- Các tổng dưới dấu $\sum$ đều có thể tính bằng cách sử dụng tổng tiền tố.

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/11458632-1709-480e-8e34-06fa7c134e6f)

- Suy ra ta tính thừa các cặp $(v_{i}, v_{j})$ cùng nằm trong một nhánh so với gốc $c$ (như hình vẽ).
- Để trừ các phần thừa này, ta xét các đỉnh $v$ nằm trong cùng một nhánh và sử dụng cách thức tương tự như phần trước, thay việc cộng vào bằng việc trừ đi.
- Sau khi tính toán xong cho gốc $c$ ta đệ quy vào các cây con $u_{i}$ và áp dụng thuật toán tương tự (chính là ý tưởng của centroid decomp).






