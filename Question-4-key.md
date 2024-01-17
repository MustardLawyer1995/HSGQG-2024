# Câu 4: Sản xuất gỗ
- Tóm tắt bài toán: Cho dãy $A$ gồm $N$ số $A[1], A[2], A[3], …, A[N]$. Có hai loại thao tác:
   - Chọn một số $x$ trong dãy, chọn hai số nguyên dương $y$ và $z$ sao cho $x = y + z$. Thực hiện xóa $x$ khỏi dãy, sau đó thêm $y$ và $z$ vào vị trí vừa xóa, đồng thời giữ nguyên thứ tự các phần tử còn lại của dãy. Thao tác này tốn chi phí $C$.
   - Chọn hai số $x$ và $y$ liền kề trong dãy. Thực hiện xóa $x$ và $y$ khỏi dãy, sau đó thêm $z = x + y$ vào vị trí vừa xóa, đồng thời giữ
- Yêu cầu bài toán: Tìm chi phí nhỏ nhất để biến đổi dãy $A$ sao cho $A$ chỉ chứa $L_{1}$ và $L_{2}$. 
## Phân tích ràng buộc bài toán
- $1 \le N \le {10^4},1 \le L_{1},L_{2} \le {10^9},1 \le C,D \le {10^5},1 \le A\left[ i \right] \le {10^9}$

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/7f1c64ac-ff8c-4bea-8be2-d2b513aa194d)

## Ví dụ minh họa: 
- $N = 3; L_{1} = 2; L_{2} = 5; C = 10; D = 4; A = [6, 5, 6]$
   - $A = [6, 5, 6]$ tốn chi phí $C = 10$
   - $A = [5, 1, 5, 6]$ tốn chi phí $C = 10$
   - $A = [5, 1, 4, 1, 6]$ tốn chi phí $D = 4$
   - $A = [5, 5, 1, 6]$ tốn chi phí $C = 10$
   - $A = [5, 5, 1, 4, 2]$ tốn chi phí $D = 4$
   - $A = [5, 5, 5, 2]$.
- Tổng chi phí: $10 + 10 + 4 + 10 + 4 = 38$.
## Phân tích từng Subtask 
### Subtask 1: $L_{1}=L_{2}$
- Đặt $L = L_{1} = L_{2}$. 
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
### Subtask 3: $N,L_{1},L_{2} ≤ 100,A[i]≤ 100$.
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
Độ phức tạp $O(N × sum(A[1], …, A[N]))$ hoặc $O(N × max(L_{1}, L_{2}, A[1], …, A[N]))$
### Subtask 4: $A[i]≤ 2024$.
- Vì $L_{1}, L_{2}$ lớn nên có thể ta phải gộp nhiều phần tử mới có thể cắt được ra $L_{1}$ hoặc $L_{2}$. 
- Ví dụ: $A = [1, 2, 4, 1, 2, 2, 1]$, cần cắt ra đoạn độ dài $L_{1} = 11$. Nếu liên tục gộp thì giá trị chiều $r$ trở nên rất lớn.  
- Cải tiến Subtask 3: Ta vẫn tính $dp[i][r]$ với $i$ là số phần tử đã gộp vào phần thừa và $r$ là độ dài phần còn thừa, tuy nhiên ta cần tính xem nếu cắt ra được được một phần tử $L_{1}$ hoặc $L_{2}$ thì ta cần phải gộp đến phần tử nào mới có thể cắt được.
- Cải tiến: $r$ là phần thừa sau khi thực hiện cắt tại ngay tại vị trí $i$, khi đó $r ≤ 2024$. Giả sử cần cắt ra một đoạn độ dài $L_{1}$:
   - $dp[i][r] → dp[x][r + sum(A[i + 1],..., A[x]) - L_{1}]$ 
   - Với $x$ là vị trí nhỏ nhất sao cho $r + sum(A[i + 1],..., A[x]) ≥ L_{1}$.
   - Tương tự với thao tác cắt một đoạn độ dài $L_{2}$.
- Vị trí $x$ có thể tìm nhanh bằng cách kỹ thuật hai con trỏ.
- Độ phức tạp: $O(N × max(A[1], …, A[N]))$.
### Subtask 5,6,7:
- Không mất tính tổng quát, ta có thể chia bài toán làm hai lượt: tách phần tử, và gộp phần tử. Xét thuật toán không tối ưu sau: 
   - Nếu ban đầu $A$ có nhiều hơn một phần tử, ta gộp tất cả thành một phần tử. Chi phí là $(n - 1) \times C$. 
   - Lúc này ta chỉ cần tách $S$ thành $x$ phần tử $L1$ và $y$ phần tử $L2$, giả sử rằng ta biết $x, y$ tối ưu. Chi phí là $(x + y - 1) \times D$
- Dễ thấy rằng thuật toán trên chỉ không tối ưu ở chỗ ta gộp toàn bộ các phần tử với nhau mà không quan tâm ở lượt sau có tách ra ở các vị trí ta đã gộp hay không. 
- Ý tưởng: Chọn trước các vị trí không cần phải gộp, bài toán trở thành tách dãy $A$ thành các dãy khác nhau. Khi tách thành các dãy con thì chúng không tương tác với nhau, ta đó xử lý riêng trên từng dãy.
- Ví dụ: 2 4 1 5|8 7 3|8 2 1 3 4 2|9
- Dùng quy hoạch động: $dp[i]$ là chi phí nhỏ nhất để biến dãy con $A[1],A[2],...,A[i]$ thành một dãy hợp lệ:
   - $dp[i] → dp[j] + cost(i + 1, j)$: chọn tách $A[i + 1],...,A[j]$ thành một dãy.
- Với $cost$ là hàm tính chi phí cho một dãy con (sẽ phân tích sau).
- Tính $cost(l, r)$: chi phí của dãy con $A[l],...,A[r]$.
   - Gộp các phần tử với nhau: $C \times (r - l)$.
   - Tách phần tử ($x$ phần tử $L_{1}$ và $y$ phần tử $L_{2}$) : $D \times (x + y - 1)$.
- Điều kiện $x, y$: 
   - $x, y ≥ 0$.
   - $L_{1} \times x + L_{2} \times y = sum(A[l],…, A[r])$.
- Dễ thấy $x, y$ là nghiệm một cặp nghiệm không âm của phương trình Diophantine sao cho $x + y$ nhỏ nhất.
- Lưu ý rằng cách tính $cost(l, r)$ này có thể không tối ưu nhưng vẫn đúng do ta đang giả sử không gộp và tách cùng một vị trí.
- Giải phương trình diophantine: $ax + by = c$.
   - Sử dụng thuật toán Euclid mở rộng để tìm $x, y$ sao cho $ax + by = gcd(a, b)$.
   - Nếu $c$ không chia hết cho $gcd(a, b)$ thì phương trình vô nghiệm.
   - Ngược lại nếu $c = k \times gcd(a, b)$, ta tìm được một nghiệm là $(x \times k, y \times k): a \times (x \times k) + b \times (y \times k) = k \times gcd(a,b) = c$.   
   - Họ nghiệm: (tìm nghiệm khác từ một nghiệm $(x_{0}, y_{0})$ đã biết)
       - $x = x_0 + k \times b / gcd(a, b)$
       - $y = y_0 -  k \times a / gcd(a, b)$
- Độ phức tạp: $O(log(max(a, b)))$.
- Quay lại bài toán, ta cần tìm $a, b$ nguyên dương sao cho $a + b$ nhỏ nhất thỏa mãn
    - $L_{1} \times a + L_{2} \times b = S = sum(A[1],...,A[N])$.
- Không mất tính tổng quát, giả sử $L_{1} ≤ L_{2}$
- Ta có thể sử dụng thuật toán tham lam: Dùng nhiều phần tử $L_{2}$ nhất có thể, giả sử ta đang dùng $a_{0}$ phần tử $L_{1}$ và $b_{0}$ phần tử $L_{2}$
- Nếu $a_{0} ≥ L_{2} / gcd(L_{1}, L_{2})$ ta luôn có một cách tốt hơn là:
    - $a = a_{0} - L_{2} / gcd(L_{1}, L_{2})$.
    - $b = b_{0} + L_{1} / gcd(L_{1}, L_{2})$.
- Do đó giá trị $a$ trong phương án tối ưu là $a$ không âm nhỏ nhất sao cho $a = a_{0} (mod L2/gcd(L_{1}, L_{2}))$
- Khi có $a$, có thể dễ dàng tìm $b = (S - a*L_{1}) / L_{2}$ 
- Xử lý tràn số: (subtask 6, 7) 
    - Do $A ≤ 109, N ≤ 104$, tổng của một dãy có thể lên đến 1013. 
    - Giá trị $(x, y)$ trả về của thuật toán Euclid mở rộng trên hai số $a, b$ có thể lên đến $O(max(a, b)) ≈ max(L_{1}, L_{2}) = 109$.
    - Nghiệm Diophantine trả về ở trên có thể lên đến $1013 × 109= 1022 > 264 - 1$.
- Ý tưởng: Lấy trước $t$ phần tử $L2$ sao cho $S - t \times L_{2} < 109$, sau đó thêm vào nghiệm với $c = S - t \times L_{2}$.










