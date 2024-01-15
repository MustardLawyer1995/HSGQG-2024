
## Câu 1: Ba đường truyền điện
Tóm tắt đề bài: Cho một bảng $N \times N$ và $M$ điểm trên bảng, điểm thứ $i$ nằm trên hàng $[A][R_i][C_i]$ có trọng số $W_i$. Cho $Q$ truy vấn độc lập, truy vấn thứ $j$ sẽ tăng giá trị của điểm thứ $T_j$ trên $D_j$. Sau khi thực hiện mỗi truy vấn, hãy chọn ra 3 hàng và cột, sao cho tổng trọng số của các ô được chọn là tốt nhất 
Note: Truy vấn độc lập là các truy vấn chỉ áp dụng lên hiện trạng ban đầu của bảng
### Subtask 1: $M,N,Q \le 40$ và $T=1$
- Ở subtask này, chúng ta có thể duyệt thủ công bằng tay ở mọi trường hợp (hàng/cột) có thể xảy ra cho mỗi truy vấn. 
- Độ phức tạp: $O(Q \times N^3)$
### Subtask 2: $M,N,Q \le 100$ và $T=1$
- Ở subtask này, chúng ta đưa ra một phán xét nhỏ: nếu tăng ô $A[i][j]$ thì khi đó đáp án của truy vấn hoặc không thay đổi, hoặc phải chứa hàng $i$, cột $j$. Lúc này ta có thể duyệt thủ công bằng tay ở 2 hàng/cột còn lại
- Độ phức tạp: $O(Q \times N^2)$
### Subtask 3: $M,N,Q \le 100$ và $T=1$
- Note: $\sum_{col}[j]=$ sum_col $[j]$
- Khi tìm cấu hình tốt nhất cho bảng, ta có 4 trường hợp: 3 hàng, 3 cột, 1 hàng + 2 cột, 1 cột + 2 hàng. Không mất tính tổng quát, chúng ta sẽ xét 2 trường hợp: 3 hàng và 1 hàng + 2 cột.
- Với trường hợp 3 hàng, ta chỉ cần đơn giản chọn ra 3 hàng có tổng lớn nhất.  
- Với trường hợp 1 hàng + 2 cột: đặt $\sum_{col}[j]$ là tổng các số trong cột thứ $j$. Ta sẽ lưu tất cả các giá trị $\sum_{col}[]$ vào một set/multiset.  
- Nếu ta chọn hàng thứ $i$, với mỗi giá trị $a[i][j]$, ta sẽ cập nhật $\sum_{col}[j] -= a[i][j]$ vào set. Sau đó, ta sẽ chọn ra 2 cột có tổng lớn nhất.  
- Dễ thấy set chỉ bị cập nhật tối đa $M$ lần, vì vậy độ phức tạp của mỗi truy vấn sẽ là $O(M \log N)$.
  ![image](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/6db86f7e-4df7-4841-aa9a-1d4e420f8acd)
