# Câu 2: Cải thiện và đánh giá 
- Tóm tắt đề bài: Quốc gia Beta gồm $N$ thành phố được kết nối bởi $M$ con đường hai chiều. $D(X, Y)$ là khoảng cách ngắn nhất từ thành phố X tới thành phố $Y$, $D(X, X) = 0$. Thành phố $Y$ tốt hơn hoặc tương đương thành phố $X$ nếu $D(Y, 1) ≤ D(X, 1)$ và $D(Y, 2) ≤ D(X, 2)$. Hạng của thành phố $X$ là số thành phố $Y$ tốt hơn hoặc tương đương với thành phố $X$ bao gồm chính nó. Gọi $P$ là phương án cải tạo, phương án thứ $j$ con đường thứ $T_j$ kết nối hai thành phố $U[T_{j}]$ và $V[T_{j}]$ sẽ được cải tạo có độ dài mới $W’[T_{j}]$ nhỏ hơn $W[T_{j}]$ ban đầu. Sau mỗi phương án, tính hạng của hai thành phố $U[T_{j}]$ và $V[T_{j}]$.
- Lưu ý: các truy vấn độc lập với nhau. 
## Phân tích ràng buộc bài toán
- $2 \le N \le {10^5},1 \le M,P \le {10^5},W\left[ i \right] \le {10^9}$
- Khi ấy ta có bảng biểu diễn chi tiết như sau:
  ![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/080180db-a7fe-42b4-bc35-348217edc98c)
