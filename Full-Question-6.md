# Câu 6: Bài tập đêm Giáng Sinh (6,0 điểm)
- Cô Tuyết chuẩn bị một bài tập đặc biệt dành cho các bạn trong đội tuyển học sinh giỏi vào giáng sinh năm nay. Đó là một bài tập về thứ tự từ điển với đề bài như sau:
- Cho một dãy số khác rỗng $C=[C_{1}, C_{2}... C_{M}]$ thỏa mãn ${C_i} \ne {C_{i - 1}},\forall i = 2,3,...M$ . Ta gọi một cách *phân đoạn đáy* là một cách chia dãy thành các đoạn con chứa các phần tử liên tiếp, mà mỗi phần tử đều thuộc đúng một đoạn con. Một cách phân đoạn dãy được coi là *hợp lệ*  nếu mỗi đoạn con chỉ chứa các phần tử đôi một phân biệt.
- Ví dụ, với $M=10$ và dãy $C=[1,2,4,3,2,1,2,8,6,8]$ thì một cách phân đoạn dãy hợp lệ là chia dãy $C$ thành 4 đoạn con lần lượt là $[1,2,4,3],[2,1],[2,8],[6,8]$ .

![image](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/4602f8af-31c9-415e-84d7-6b56326c9233)

- Một cách phân đoạn hợp lệ khác là chia dãy $C$ thành 5 đoạn con lần lượt là $[1,2,4], [3,2,1], [2,8], [6], [8]$ .

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/b63f87ae-54fd-4a8f-a7cd-ee2b8f064d97)
  
- Cả hai cách phân đoạn dãy trên đều thỏa mãn mọi đoạn con chỉ chứa các phần tử đôi một phân biệt. Mặt khác, nếu ta chia dãy $C$ thành 4 đoạn con lần lượt là $[1], [2,4,3,2,1,2], [8], [6], [8]$ thì cũng không hợp lệ bởi có ba phần tử cùng bằng 2 trong đoạn con thứ hai.
- Mỗi dãy có thể có nhiều cách phân đoạn dãy hợp lệ. Mỗi cách phân đoạn dãy được mã hóa bằng một *mã hóa phân đoạn* $A=[A_{1}, A_{2}, ....,A_{K}]$ , với $K$ là số lượng đoạn con, và $A_{i}$ là số lượng phần tử của đoạn con thứ $i$. Chẳng hạn, với $M=10$ và dãy $C=[1,2,4,3,2,1,8,6,8]$ thì cách phân đoạn dãy trong hình đầu tiên sẽ được mã hóa bằng dãy $A=[4,2,2,2]$ .

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/34908f0d-ec58-4a9d-8711-348a5849d9c4)

- Tương tự, cách phân đoạn dãy trong hình thứ hai sẽ được mã hóa thành dãy $A=[3,3,2,1,1]$ .

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/057f1819-816d-45a4-83a6-030205e831c4)

- Cô Tuyết viết lên bảng một dãy số khác rỗng $C=[C_{1}, C_{2}... C_{M}]$ thỏa mãn ${C_i} \ne {C_{i - 1}},\forall i = 2,3,...M$ , rồi lại viết lên bảng thêm hai số nguyên dương $X$ và $Y$ . Sau đó gọi một bạn lên bảng để trả lời câu hỏi sau:
- "Khi liệt kê tất cả các dãy mã hóa phân đoạn của dãy $C$ rồi sắp xếp chúng theo thứ tự từ điển ngược thì dãy mã hóa phân đoạn thứ $X$ và dãy mã hóa phân đoạn thứ $Y$ có độ dài tiền tố chung dài nhất là bao nhiêu ?" .
    - Nhắc lại (1): Một dãy mã hóa phân đoạn $U=[U_{1}, U_{2}, .... U_{K}]$ gọi là đi trước dãy mã hóa phân đoạn $V=[V_{1}, V_{2}, .... V_{H}]$ theo *thứ tự từ điển ngược* nếu thỏa mãn một trong hai điều kiện sau:
       - $K>H$ và $U_{i}=V_{i}, \forall i = 1,2,....H$ ;
       - Tồn tại $1 \le T \le min(K,H)$ sao cho $U_{i}=V_{i} , \forall i = 1,2,....T-1$ và $U_{T}>V_{T}$
    - Dãy số $U=[U_{1}, U_{2}, .... U_{K}]$ được gọi là *tiền tố* độ dài $K$ của dãy $V=[V_{1}, V_{2}, .... V_{H}]$ khi và chỉ khi $K \le H$ và $U_{i}=V_{i} , \forall i = 1,2,....K$ . Lưu ý, dãy rỗng (kí hiệu là $[]$) là tiền tó có độ dài bằng $0$ của mọi dãy số.
    - Nhắc lại (2): *Tiền tố chung dài nhất* của hai dãy số $Z_{1}$ và $Z_{2}$ là dãy số có độ dài lớn nhất vừa là tiền tố của dãy $Z_{1}$ vừa là tiền tố của dãy $Z_{2}$ .
- Nhận thấy rằng nếu chỉ đặt ra câu hỏi cho một cặp số $(X,Y)$ thì bài toán chưa đủ khó, cô Tuyết quyết định thêm vào một vài tham số mới. Cô gọi $Q$ bạn lần lượt lên bảng, bạn thứ $i$ sẽ nhận được 4 số $L_{i}, R_{i}, X_{i}, Y_{i}$ và có nhiệm vụ trả lời câu hỏi sau:
- "Khi liệt kê tất cả các dãy mã hóa phân đoạn của dãy $C' = \left[ {{C_{{L_i}}},{C_{{L_i} + 1}},....,{C_{{R_i}}}} \right]$ rồi sắp xếp chúng theo thứ tự từ điển ngược thì dãy mã hóa phân đoạn thứ $X_{i}$ và dãy mã hóa phân đoạn thứ $Y_{i}$ có độ dài tiền tố chung dài nhất là bao nhiêu ?".
- Yêu cầu: Hãy giúp các bạn trả lời $Q$ câu hỏi của cô Tuyết.
### Dữ liệu: Vào từ file văn bản NOEL.INP
- Dòng đầu chứa hai số nguyên $M$ và $Q$ lần lượt là độ dài của dãy $C$ và số lượng bạn được cô Tuyết gọi lên bảng: $1 \le M,Q \le 2 \times 10^{5}$ .
- Dòng thứ hai chứa $M$ số nguyên $C_{1}, C_{2}... C_{M}$ với $1 \le C_{i} \le M , \forall i = 1,2,...M$ và ${C_i} \ne {C_{i - 1}},\forall i = 2,3,...M$ .
- Dòng thứ $i$ trong số $Q$ dòng tiếp theo biểu diễn một câu hỏi với 4 số nguyên $L_{i}, R_{i}, X_{i}, Y_{i}$ với $1 \le L_{i} \le R_{i} \le M$ và $1 \le X_{i} \le Y_{i} \le 10^{17}$ . Dữ liệu đảm bảo số lượng dây mã hóa phân đoạn của dãy $C' = \left[ {{C_{{L_i}}},{C_{{L_i} + 1}},....,{C_{{R_i}}}} \right]$ không nhỏ hơn $\text{max} (X_{i},Y_{i})$ .
- Các số trên cùng một dòng cách nhau bởi dấu cách.
### Kết quả: Ghi ra file văn bản NOEL.OUT:
- Gồm $Q$ dòng, trong đó dòng thứ $i$ chứa một số nguyên là độ dài tiền tố chung dài nhất của hai dãy mã hóa phân đoạn của dãy $C' = \left[ {{C_{{L_i}}},{C_{{L_i} + 1}},....,{C_{{R_i}}}} \right]$ , với dãy mã hóa thứ nhất có thứ tự từ điển ngược bằng $X_{i}$ và dãy mã hóa thứ hai có thứ tự từ điển ngược bằng $Y_{i}$ .
### Ví dụ: 

![image](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/be88393a-b67b-463a-9539-fca3be5d0377)

### Ràng buộc: 
- (1) Có 17.5% số test ứng với 17.5% số điểm thỏa mãn: $M \le 12$ và $Q \le 2024$ .
- (2) 22.5% số test khác ứng với 20% số điểm thỏa mãn: $X_{i}=Y_{i}=1, \forall i =1,2,...Q$ .
- (3) 22.5% số test khác ứng với 22.5% số điểm thỏa mãn: $L_{i}=1 ; R_{i}=M$ và $X_{i}, Y_{i} \le 10^{5} , \forall i =1,2,...Q$ .
- (4) 22.5% số test khác ứng với 22.5% số điểm thỏa mãn: $M \le 2000$ và $Q \le 20000$ .
- (5) 17.5% số test còn lại ứng với 17.5% số điểm: không có ràng buộc gì thêm. 








