
## Câu 1: Ba đường truyền điện
Tóm tắt đề bài: Cho một bảng $N \times N$ và $M$ điểm trên bảng, điểm thứ $i$ nằm trên hàng $[A][R_i][C_i]$ có trọng số $W_i$. Cho $Q$ truy vấn độc lập, truy vấn thứ $j$ sẽ tăng giá trị của điểm thứ $T_j$ trên $D_j$. Sau khi thực hiện mỗi truy vấn, hãy chọn ra 3 hàng và cột, sao cho tổng trọng số của các ô được chọn là tốt nhất 
Note: Truy vấn độc lập là các truy vấn chỉ áp dụng lên hiện trạng ban đầu của bảng
### Subtask 1: $\[M,N,Q \le 40\]$ và $T=1$
- Ở subtask này, chúng ta có thể duyệt thủ công bằng tay ở mọi trường hợp (hàng/cột) có thể xảy ra cho mỗi truy vấn. 
- Độ phức tạp: $O(Q \times N^3)$

