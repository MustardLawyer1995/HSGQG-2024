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

## Phân tích các Subtask: 
