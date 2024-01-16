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
### Subtask 3: $N,L1,L2 ≤ 100,A[i]≤ 100$.
- Để đơn giản ta sẽ luôn giữ phần thừa của các phần tử phía trước. Khi gặp một phần tử mới ta luôn gộp vào phần thừa, và ta chỉ tách nếu nó tạo ra một phần tử hợp lệ. 
   - $A = [6, 5, 6]$ còn thừa 0
   - $A = [6, 5, 6]$ gộp 6 vào phần thừa, còn thừa 6 (không tốn chi phí)
   - $A = [6, 5, 6]$ cắt ra một đoạn 5, còn thừa 1
   - $A = [6, 5, 6]$ gộp 5 vào phần thừa, còn thừa 6
   - $A = [6, 5, 6]$ cắt ra một đoạn 5, còn thừa 1
   - $A = [6, 5, 6]$ gộp 6 vào phần thừa, còn thừa 7
   - $A = [6, 5, 6]$ cắt ra một đoạn 5, còn thừa 2
   - $A = [6, 5, 6]$ cắt ra một đoạn 2, còn thừa 0 (không tốn chi phí)
- Quy hoạch động: tính $dp[i][r]$ với $i$ là số phần tử đã gộp vào phần thừa và $r$ là độ dài phần còn thừa
   - $dp[i][r] → dp[i + 1][r + A[i]]$
   - $dp[i][r] → dp[i][r - L1]$
   - $dp[i][r] → dp[i][r - L2]$
   - $dp[0][0] = 0$
   - --> Kết quả: $dp[n][0]$
Độ phức tạp $O(N × sum(A[1], …, A[N]))$ hoặc $O(N × max(L1, L2, A[1], …, A[N]))$
### Subtask 4: $A[i]≤ 2024$.
- Vì $L1, L2$ lớn nên có thể ta phải gộp nhiều phần tử mới có thể cắt được ra $L1$ hoặc $L2$. 
- Ví dụ: $A = [1, 2, 4, 1, 2, 2, 1]$, cần cắt ra đoạn độ dài $L1 = 11$. Nếu liên tục gộp thì giá trị chiều $r$ trở nên rất lớn.  
- Cải tiến Subtask 3: Ta vẫn tính $dp[i][r]$ với $i$ là số phần tử đã gộp vào phần thừa và $r$ là độ dài phần còn thừa, tuy nhiên ta cần tính xem nếu cắt ra được được một phần tử $L1$ hoặc $L2$ thì ta cần phải gộp đến phần tử nào mới có thể cắt được.
- Cải tiến: $r$ là phần thừa sau khi thực hiện cắt tại ngay tại vị trí $i$, khi đó $r ≤ 2024$. Giả sử cần cắt ra một đoạn độ dài $L1$:
   - $dp[i][r] → dp[x][r + sum(A[i + 1],..., A[x]) - L1]$ 
   - Với $x$ là vị trí nhỏ nhất sao cho $r + sum(A[i + 1],..., A[x]) ≥ L1$.
   - Tương tự với thao tác cắt một đoạn độ dài $L2$.
- Vị trí $x$ có thể tìm nhanh bằng cách kỹ thuật hai con trỏ.
- Độ phức tạp: $O(N × max(A[1], …, A[N]))$.
### Subtask 5,6,7:
- Không mất tính tổng quát, ta có thể chia bài toán làm hai lượt: tách phần tử, và gộp phần tử. Xét thuật toán không tối ưu sau: 
   - Nếu ban đầu A có nhiều hơn một phần tử, ta gộp tất cả thành một phần tử. Chi phí là (n - 1) * C 
   - Lúc này ta chỉ cần tách S thành x phần tử L1 và y phần tử L2, giả sử rằng ta biết x, y tối ưu. Chi phí là (x + y - 1) * D
- Dễ thấy rằng thuật toán trên chỉ không tối ưu ở chỗ ta gộp toàn bộ các phần tử với nhau mà không quan tâm ở lượt sau có tách ra ở các vị trí ta đã gộp hay không. 








