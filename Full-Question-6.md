# Câu 5: Mạng truyền tin (7,0 điểm)
- Một mạng truyền tin có $N$ máy tính, các máy tính được đánh số từ $1$ đến $N$ . Có $N-1$ dây cáp, được đánh số từ $1$ đến $N-1$ . Dây cáp thứ $i$ nối máy tính $u_{i}$ với máy tính $v_{i}$ và có giới hạn truyền tải $w_{i}$ . Các dây cáp bảo đảm từ một máy tính bất kì có thể truyển tin đi qua một số máy tính và dây cáp nào đó. Khi hai máy tính truyền tin cho nhau, chúng sẽ luôn sử dụng đường truyền tin sao cho không sử dụng dây cáp nào quá một lần. Độ lớn của gói tin truyền đi phải không lớn hơn giới hạn truyền tải của mọi dây cáp mà nó sử dụng. Chi phí để truyền một gói tin giữa hai máy tính bằng kích thước của gói tin nhân với bình phương số lượng dây cáp trên đường truyền tin.
- Người ta muốn chọn ra một máy tính $r$ để làm máy chủ. Khi đó, máy tính $r$ sẽ truyền tin đến tất cả các máy tính khác. Vì phải dự trù cho mọi trường hợp, ta cần phải xét chi phí truyền tin tối đa. *Chi phí truyền tin tối đa* giữa máy tính $r$ và máy tính $x$ là $C_{min}(r,x) \times (D(r,x))^2$ trong đó $C_{min}(r,x)$ là giới hạn truyền tải nhỏ nhất trong số các giới hạn truyền tải của các dây cáp trên đường truyền tin giữa máy tính $r$ và máy tính $x$ , $(D(r,x))^2$ là số dây cáp trên đường truyền tin giữa máy tính $r$ và máy tính $x$ . *Chi phí vận hành mạng* là tổng của chi phí truyền tin tối đa giữa máy tính $r$ và tất cả các máy tính khác.
- **Yêu cầu**: Với mỗi $r=1,2,...N$ , hãy tính chi phí vận hành mạng nếu chọn máy tính $r$ làm máy chủ.
### Dữ liệu: Vào từ file văn bản NETW.INP
   - Dòng đầu chứa một số nguyên $N$ là số lượng máy tính: $1 \le N \le {10^5}$
   - Dòng thứ $i$ trong số $N-1$ dòng tiếp theo chứa ba số nguyên $u_{i}, v_{i}$ và $w_{i}$ cho biết có một dây cáp nối máy tính $u_{i}$ với máy tính $v_{i}$ và có giới hạn truyền tải là $w_{i}$ : $1 \le {u_i},{v_i} \le N;1 \le {w_i} \le {10^9}$ .
- Các số trên cùng một dòng cách nhau bởi dấu cách.
### Kết quả: Ghi ra file văn bản NETW.OUT
- Gồm $N$ dòng, trong đó dòng thứ $r$ chứa một số nguyên là phần dư của chi phí vận hành mạng nếu chọn máy tính $r$ làm máy chủ trong phép chia cho 998244353.
### Ví dụ: 


### Giải thích: 
- Chi phí truyền tin tối đa giữa tất cả các cặp máy tính được cho trong bảng sau:

- Có 4 dây cáp trên đường truyền tin giữa máy tính 3 và máy tính 7 với giới hạn truyền tải là 2,3,2,2 vì vậy $C_{min} (3,7) = 2$ và $D(3,7)=4$ . Chi phí truyền tin tối đa giữa 3 và 7 là $2 \times 4^{2} = 32$ , do đó số ở vị trí tương ứng với $r=3$ và $x=7$ trong bảng trên là 32.
- Chi phí vận hành nếu chọn máy tính 4 làm máy chủ là $8+2+18+1+4+2=35$ , do đó số ở cột cuối cùng ứng với $r=4$ trong bảng trên là 35.
### Ràng buộc: 
- (1) Có 16% số test ứng với 16% số điểm thỏa mãn: $N \le 5000$
- (2) 12% số test khác ứng với 12% số điểm thỏa mãn: $w_{i} \le 2$ và luôn có dây cáp nối giữa máy tính $i$ và máy tính $i+1$ , $\forall i = 1,2,...N-1$ .
- (3) 20% số test khác ứng với 20% số điểm thỏa mãn: $w_{i} = 1$ , $\forall i = 1,2,...N-1$ .
- (4) 16% số test khác ứng với 16% số điểm thỏa mãn: $w_{i} \le 1000$ , $\forall i = 1,2,...N-1$ .
- (5) 16% số test khác ứng với 16% số điểm thỏa mãn: luôn có dây cáp nối giữa máy tính $i$ và máy tính $i+1$ , $\forall i = 1,2,...N-1$ .
- (6) 20% số test còn lại ứng với 20% số điểm: không có ràng buộc gì thêm.
