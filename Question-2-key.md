# Câu 2: Cải thiện và đánh giá 
- Tóm tắt đề bài: Quốc gia Beta gồm $N$ thành phố được kết nối bởi $M$ con đường hai chiều. $D(X, Y)$ là khoảng cách ngắn nhất từ thành phố X tới thành phố $Y$, $D(X, X) = 0$. Thành phố $Y$ tốt hơn hoặc tương đương thành phố $X$ nếu $D(Y, 1) ≤ D(X, 1)$ và $D(Y, 2) ≤ D(X, 2)$. Hạng của thành phố $X$ là số thành phố $Y$ tốt hơn hoặc tương đương với thành phố $X$ bao gồm chính nó. Gọi $P$ là phương án cải tạo, phương án thứ $j$ con đường thứ $T_j$ kết nối hai thành phố $U[T_{j}]$ và $V[T_{j}]$ sẽ được cải tạo có độ dài mới $W’[T_{j}]$ nhỏ hơn $W[T_{j}]$ ban đầu. Sau mỗi phương án, tính hạng của hai thành phố $U[T_{j}]$ và $V[T_{j}]$.
- Lưu ý: các truy vấn độc lập với nhau. 
## Phân tích ràng buộc bài toán
- $2 \le N \le {10^5},1 \le M,P \le {10^5},W\left[ i \right] \le {10^9}$
- Khi ấy ta có bảng biểu diễn chi tiết như sau:

  ![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/080180db-a7fe-42b4-bc35-348217edc98c)
## Phân tích từng Subtask
### Subtask 1: $M,P \le 1000$
- Với mỗi phương án cải tạo, ta thực hiện thuật toán đường đi ngắn nhất - Dijkstra từ hai thành phố 1 và 2 để tìm đường đi ngắn nhất tới mọi thành phố còn lại. Khi đã có khoảng cách ngắn nhất tới mỗi thành phố, để tính hạng của thành phố $U[T_{j}]$ và $V[T_{j}]$, ta xét lần lượt từng thành phố và kiểm tra xem thành phố này có tốt hơn hoặc tương đương hai thành phố trong phương án cải tạo không.
- Độ phức tạp: $O\left( {P \times \left( {M\log N + N} \right)} \right)$
### Subtask 4: $M=N-1$
- Vì đồ thị liên thông nên khi đó đồ thị có dạng cây.

  ![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/01713c24-7908-41bf-8112-b822602965ef)

- Xét lần lượt 2 cây có gốc là đỉnh 1 và đỉnh 2. 
- Ta thấy rằng nếu khoảng cách tới đỉnh $u$ giảm đi, thì khoảng cách những đỉnh thuộc cây con gốc $u$ cũng sẽ giảm, tuy nhiên vẫn lớn hơn của $u$, các đỉnh còn lại không ảnh hưởng.  Vì vậy để tính hạng của $u$, ta chỉ cần dựa vào những đỉnh có khoảng cách nhỏ hơn $u$ hiện tại ở đồ thị ban đầu.
- Để tính hạng của đỉnh $U$ sau khi đường đi được cải tạo, ta tính các giá trị $D’(U, 1), D’(U, 2)$. Sau đó sắp xếp các truy vấn và các đỉnh của đồ thị ban đầu theo khoảng cách so với đỉnh 1.
- Xét các đỉnh và truy vấn tăng dần theo khoảng cách tới đỉnh 1, nếu có cùng khoảng cách tới đỉnh 1, ta ưu tiên các đỉnh trong đồ thị ban đầu đứng trước các truy vấn, có $F[i]$ là số lượng đỉnh trong đồ thị ban đầu có $D(X, 2) = i$.
- Khi xét tới một truy vấn, vì điều kiện $D(X, 1) ≤ D’(U, 1)$ đã thỏa mãn, khi đó hạng của đỉnh $U$ là tổng $F[i]$ với $i ≤ D’(U, 2)$.
- Để giảm bộ nhớ và tăng tốc các thao tác cập nhật, tính tổng mảng $F$, ta nén các giá trị khoảng cách tới đỉnh 2, sau đó sử dụng cấu trúc dữ liệu IT / BIT.
- Độ phức tạp: $O\left( {\left( {N + P} \right)\log \left( {N + P} \right)} \right)$

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/05406061-3342-440d-8548-2f9e3267c883)

- Trước hết xét đỉnh có khoảng cách tới đỉnh 1 và 2 lần lượt là 0, 2.
- Khi đó ta có: F[2] += 1;

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/9b5d976f-3a80-41c2-9bf2-ede6fcf074ef)

- Tiếp đến xét đỉnh có khoảng cách tới đỉnh 1 và 2 lần lượt là 1, 3.
- Khi đó ta có: F[3] += 1;

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/61da2156-621b-46b7-945c-680d7c66206d)

- Tiếp đến xét đỉnh có khoảng cách tới đỉnh 1 và 2 lần lượt là 2, 0.
- Khi đó ta có: F[0] += 1;

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/2bda98e2-9ba8-4026-af2c-6b7589db959c)

- Tiếp đến xét truy vấn tính hạng đỉnh $U$ có khoảng cách mới tới đỉnh 1 và 2 lần lượt là 2, 4.
- Khi đó ta có hạng của đỉnh $U$ là: F[0] + F[1] + F[2] + F[3] +  F[4] = 3.

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/51c37c34-fd3f-4737-aa46-d06d350ed988)

- Tiếp đến xét đỉnh có khoảng cách tới đỉnh 1, 2 lần lượt là 4, 6.
- Khi đó ta có: F[6] += 1;

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/20e8db9f-68b0-4c5c-9e7c-2191dd045cd4)

- Tiếp đến xét truy vấn tính hạng đỉnh U có khoảng cách mới tới đỉnh 1 và 2 lần lượt là 4, 2.
- Khi đó ta có hạng của đỉnh $U$ là: F[0] + F[1] + F[2] = 2.

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/20c93486-61b3-4165-a070-ec3255db3c42)

- Cuối cùng xét đỉnh có khoảng cách tới đỉnh 1, 2 lần lượt là 5, 3.
- Khi đó ta có: F[3] += 1;

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/d157bdf0-2b23-480e-9f15-ae5fc63cbbba)

### Subtask 2,3,5: 
- Thực hiện thuật toán dijkstra từ hai đỉnh 1, 2 để tính khoảng cách ngắn nhất tới mọi đỉnh còn lại. 
- Khi con đường nối giữa hai đỉnh $U, V$ được cải tạo, ta có:
   - $D(U, 1) = min(D(U, 1), D(V, 1) + W’(U, V))$.
   - $D(U, 2) = min(D(U, 2), D(V, 2) + W’(U, V))$.
   - $D(V, 1) = min(D(V, 1), D(U, 1) + W’(U, V))$.
   - $D(V, 2) = min(D(V, 2), D(U, 2) + W’(U, V))$.
- Tính hạng của đỉnh $U$:
   - Ta có các nhận xét như sau:
       - Các đỉnh có đường đi ngắn nhất trên đồ thị mới đi qua con đường $(U, V)$ sẽ có khoảng cách lớn hơn U nên sẽ không ảnh hưởng đến hạng của $U$.
       - Các đỉnh có đường đi ngắn nhất trên đồ thị không đi qua con đường $(U, V)$ nên khi đó độ dài đường đi ngắn nhất bằng độ dài đường đi ngắn nhất trên đồ thị ban đầu.
   - Khi đó hạng của đỉnh $U$ sẽ phụ thuộc vào những đỉnh có $D(X, 1) ≤ D’(U, 1)$ và $D(X, 2) ≤ D’(U, 2)$ trên đồ thị ban đầu, ta sắp xếp lại như subtask 4 và trả lời truy vấn offline.
- Độ phức tạp: $O\left( {M\log N + \left( {N + P} \right)\log \left( {N + P} \right)} \right)$
 












