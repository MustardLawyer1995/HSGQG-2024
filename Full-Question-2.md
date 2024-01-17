# Câu 2: Cải thiện đánh giá 
- Quốc gia Beta có $N$ thành phố được đánh số từ 1 đến $N$. Các thành phố được nối với nhau bởi $M$ con đường hai chiều, được đánh số từ 1 đến $M$, giữa hai thành phố bất kỳ có tối đa một con đường nối trực tiếp chúng. Con đường hai chiều số $i(1 \leq i \leq M)$ nối trực tiếp giữa hai thành phố phân biệt $U_{i}$ và $V_{i}$ có độ dài $W_{i}$. Một *đường đi* gồm $K$ thành phố tữ thành phố $X$ tới thành phố $Y$ là một chuỗi cạc thành phố $P_{1}, P_{2}, \ldots, P_{K}$, sao cho $P_{1}=X, P_{K}=Y$ và có con đường trực tiếp giữa hai thành phố $P_{i}$ và $P_{i+1}(\forall i=1,2, \ldots, K-1)$. Ở quốc gia Beta, mọi thành phố đèu có đường đi tới thành phố khác. *Chi phí di chuyển* của một đường đi từ thành phố $X$ tới thành phố $Y$ là tổng độ dài của các con đường trên đường đi đó. Gọi $D(X, Y)$ là chi phí di chuyển nhỏ nhất trong số các chi phí di chuyển của các đường đi từ thành phố $X$ tới thành phố $Y$. Quy ước $D(X, X)=0$ với mọi thành phố $X$.  
- Thành phố số 1 có một nhà máy đúc khuôn và thành phố số 2 có một nhà máy sản xuất mạ tĩnh điện. Một doanh nghiệp muốn chọn một thành phố nào đó để mở một trung tâm chế tạo thép trang trí sử dụng nguyên liệu từ nhà máy đúc khuôn và nhà máy sản xuất mạ tĩnh điện. Thành phố $Y$ được gọi là *tốt hơn hoặc tương đương* so với thành phố $X$ khi và chỉ khi $D(Y, 1) \leq D(X, 1)$ và $D(Y, 2) \leq D(X, 2)$. Lưu ý, thành phố $X$ được xem là tốt hơn hoặc tương đương so với chính nó. Doanh nghiệp tính *hạng* của thành phố $X$ là số lượng thành phố $Y$ tốt hơn hoặc tương đương so với thành phố $X$. Cụ thể, công thức tính hạng là:  
```math 
R(X)=\mid\{Y \in\{1,2, \ldots, N\}: D(Y, 1) \leq D(X, 1) \text { và } D(Y, 2) \leq D(X, 2)\} \mid .  
``` 
- Ngoài ra, doanh nghiệp cũng cam kết với chính quyền địa phương rằng trước khi đặt trung tâm chế tạo thép ở thành phố $X$ nào đó, họ sẽ cải tạo một con đường nối với thành phố $X$. Doanh nghiệp đã khảo sát và đưa ra $P$ phương án. Với phương án thứ $j$ $(1 \leq j \leq P)$, con đường $T_{j}$ nối giữa thành phố $U_{T_{j}}$ và $V_{T_{j}}$ sẽ được chọn để cải tạo giúp cho độ dài mới $W_{T_{j}}^{\prime}$ bé hơn độ dài ban đầu $W_{T_{j}}$. Với mỗi phương án, sau khi cải tạo đường, doanh nghiệp cần tính hạng của thành phố $U_{T_{j}}$ và thành phố $V_{T_{j}}$. Các phương án là độc lập, nghĩa là các phương án đều chỉ áp dụng lên hiện trạng ban đầu của $M$ con đường.  
- Yêu cầu: Với phương án thứ $j(1 \leq j \leq P)$, hãy giúp doanh nghiệp tìm ra hạng của thành phố $U_{T_{j}}$ và thành phố $V_{T_{j}}$ sau khi cải tạo con đường $T_{j}$.
### Dữ liệu: Vào từ file văn bản IMPEVAL.INP
- Dòng đầu chứa ba số nguyên $N, M$ và $P$ lần lượt là số lượng thành phố, số lượng con đường và số lượng phương án $\left(2 \leq N \leq 10^{5} ; 1 \leq M, P \leq 10^{5}\right)$.  
- Dòng thứ $i$ trong số $M$ dòng tiếp theo chứa ba số nguyên $U_{i}\left(V_{i}\right)$ và $W_{i}$ lần lượt là hai thành phố được nối bởi con đường số $i$ và độ dài của con đường năy $\left(1 \leq U_{i}, V_{i} \leq N ; 1 \leq W_{i} \leq 10^{9}\right)$.
- Dòng thứ $j$ trong số $P$ dòng tiếp theo chứa hai số nguyên $T_{j}$ và $W_{T_{j}}^{\prime}$ lần hượt là chỉ số con đường được lên phương án cải tạo và độ dài sau khi cải tạo ($1 \le {T_j} \le M$ và $1 \le {W_{{T_j}}}^\prime  < {W_{{T_j}}}$).
- Các số trên cùng một dòng cách nhau bởi dấu cách. 
### Kết quả: Ghi ra file văn bản IMPEVAL.OUT
- Gồm $P$ dòng, trong đó dòng thứ $j$ ghi ra hai số nguyên $R\left(U_{T_{j}}\right)$ và $R\left(V_{T_{j}}\right)$ tương ứng là hạng của thành phố $U_{T_{j}}$ và thành phố $V_{T_{j}}$ nếu phương án thứ $j$ được triển khai.
### Ràng buộc: 
   - (1) Có 20% số test ứng với 20% số điểm thỏa mãn: $M, P \leq 1000$.
   - (2) 20% số test khác ứng với 20% số điểm thỏa mān: Mỗi thành phố có nhiều nhất 2 con đường nối với thành phố khác.
   - (3) 20% số test khác ứng với 20% số điểm thỏa mãn: Mọi con đường đều nối với thành phố số 1 hoặc thành phố số 2.
   - (4) 20% số test khác ứng với 20% số điểm thỏa mãn: $M=N-1$.   
   - (5) 20% số test còn lại ứng với 20% số điểm: Không có ràng buộc gì thêm.
### Ví dụ:

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/b07556a4-3e4c-4b4f-8e30-dbbdd566fe72)















