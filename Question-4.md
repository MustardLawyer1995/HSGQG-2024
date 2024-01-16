# Câu 4: Sản xuất gỗ
- Tóm tắt bài toán: Cho dãy $A$ gồm $N$ số $A[1], A[2], A[3], …, A[N]$. Có hai loại thao tác:
   - Chọn một số $x$ trong dãy, chọn hai số nguyên dương $y$ và $z$ sao cho $x = y + z$. Thực hiện xóa $x$ khỏi dãy, sau đó thêm $y$ và $z$ vào vị trí vừa xóa, đồng thời giữ nguyên thứ tự các phần tử còn lại của dãy. Thao tác này tốn chi phí $C$.
   - Chọn hai số $x$ và $y$ liền kề trong dãy. Thực hiện xóa $x$ và $y$ khỏi dãy, sau đó thêm $z = x + y$ vào vị trí vừa xóa, đồng thời giữ
- Yêu cầu bài toán: Tìm chi phí nhỏ nhất để biến đổi dãy $A$ sao cho $A$ chỉ chứa $L1$ và $L2$. 
## Phân tích ràng buộc bài toán
- $1 \le N \le {10^4},1 \le L1,L2 \le {10^9},1 \le C,D \le {10^5},1 \le A\left[ i \right] \le {10^9}$

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/7f1c64ac-ff8c-4bea-8be2-d2b513aa194d)

## Ví dụ minh họa: 
- $N = 3; L1 = 2; L2 = 5; C = 10; D = 4; A = [6, 5, 6]$
   - $A = [6, 5, 6]$ tốn chi phí $C = 10$
   - $A = [5, 1, 5, 6]$ tốn chi phí $C = 10$
   - $A = [5, 1, 4, 1, 6]$ tốn chi phí $D = 4$
   - $A = [5, 5, 1, 6]$ tốn chi phí $C = 10$
   - $A = [5, 5, 1, 4, 2]$ tốn chi phí $D = 4$
   - $A = [5, 5, 5, 2]$.
- Tổng chi phí: $10 + 10 + 4 + 10 + 4 = 38$.
## Phân tích từng Subtask 
### Subtask 1: $L1=L2$
- Đặt $L = L1 = L2$. 
- Vì dãy cuối cùng chỉ có một giá trị $L$, ta chỉ cần liên tục ghép hoặc tách phần tử:
   - Bắt đầu từ đầu dãy, gọi $i$ là vị trí đầu tiên mà $A[i] != L$. 
        - Nếu $A[i] < L$, ta ghép $A[i]$ với $A[i + 1]$.
        - Nếu $A[i] > L$, ta tách $A[i]$ thành $L$ và $A[i] - L$.
   - Thuật toán dừng lại khi $i = n$, lúc này ta chỉ cần kiểm tra xem dãy $A$ có toàn $L$ hay không.
- Độ phức tạp: $O(N)$
### Subtask 2: Tổng các phần tử của dãy $A ≤ 20$.
- Đặt $S = \sum A[i]$
- Vì $S ≤ 20$, ta có thể lưu dãy $A$ dưới dạng dãy nhị phân $S - 1$ bit. Đưa về bài toán trên đồ thị có hướng. Khi đó ta có thể sử dụng thuật toán Dijkstra để tìm chi phí nhỏ nhất. Cách lưu như sau: $A = [4, 3, 2] → o o o o|o o o|o o →  00010010$.
- Độ phức tạp: $O(2^{S} × S^2)$ với hằng số nhỏ

- Cải tiến: Dùng kĩ thuật BFS với 2 queue, mỗi queue cho một loại trọng số cạnh.
- Độ phức tạp: $O(2^{S} × S)$



