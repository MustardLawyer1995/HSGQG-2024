# Câu 4: Sản xuất gỗ
- Tóm tắt bài toán: Cho dãy $A$ gồm $N$ số $A[1], A[2], A[3], …, A[N]$. Có hai loại thao tác:
   - Chọn một số $x$ trong dãy, chọn hai số nguyên dương $y$ và $z$ sao cho $x = y + z$. Thực hiện xóa $x$ khỏi dãy, sau đó thêm $y$ và $z$ vào vị trí vừa xóa, đồng thời giữ nguyên thứ tự các phần tử còn lại của dãy. Thao tác này tốn chi phí $C$.
   - Chọn hai số $x$ và $y$ liền kề trong dãy. Thực hiện xóa $x$ và $y$ khỏi dãy, sau đó thêm $z = x + y$ vào vị trí vừa xóa, đồng thời giữ
- Yêu cầu bài toán: Tìm chi phí nhỏ nhất để biến đổi dãy $A$ sao cho $A$ chỉ chứa $L1$ và $L2$. 
## Phân tích ràng buộc bài toán
- $1 \le N \le {10^4},1 \le L1,L2 \le {10^9},1 \le C,D \le {10^5},1 \le A\left[ i \right] \le {10^9}$

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/7f1c64ac-ff8c-4bea-8be2-d2b513aa194d)

## Ví dụ minh họa: 
- N = 3; L1 = 2; L2 = 5; C = 10; D = 4; A = [6, 5, 6]
   - A = [6, 5, 6] tốn chi phí C = 10
   - A = [5, 1, 5, 6] tốn chi phí C = 10
   - A = [5, 1, 4, 1, 6] tốn chi phí D = 4
   - A = [5, 5, 1, 6] tốn chi phí C = 10
   - A = [5, 5, 1, 4, 2] tốn chi phí D = 4
   - A = [5, 5, 5, 2]
- Tổng chi phí: 10 + 10 + 4 + 10 + 4 = 38
## Phân tích từng Subtask 
### Subtask 1: $L1=L2$
