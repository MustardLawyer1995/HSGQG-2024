# Câu 3: Thu mua nông sản (6,0 điểm)
- Quốc gia Delta có nền nông nghiệp hàng đầu thế giới. Năm nay, nhờ ứng dụng công nghệ thông tin sâu rộng trong sản xuất nông nghiệp, nông dân quốc gia Delta đã được mùa lớn. Để chúc mừng thành công lớn của bà con cũng như đẩy mạnh việc xuất khẩu, chính phủ quyết định bố trí các xe thu mua nông sản từ khắp mọi nơi trên cả nước.  
- Trong quốc gia có $N$ ngôi làng được đánh số từ 1 đến $N$. Mạng lưới giao thông tại đây gồm $N-1$ con đường hai chiều, mỗi con đường nối trực tiếp hai ngôi làng nào đó. Các con đường này bāo đảm sự liên thông toàn quốc. Nói cách khác, từ một ngôi làng bất kỳ có thể đi tới tất cả các ngồi làng còn lại thông qua một hoặc nhiều con đường. Người dân tại quốc gia Delta có khả năng sản xuất được $K$ loại nông sản khác nhau, được đánh số từ 1 đến $K$. Năm nay, người dân tại ngôi làng thứ $i(1 \leq i \leq N)$ sản xuất loại nông sản thứ $A_{i-1}$.  
- Chính phủ quốc gia Delta sẽ bố trí $\frac{N \times (N-1)}{2}$ xe tải đi thu mua nông sản. Cụ thể, với mỗi cặp số nguyên $(u, v)$ sao cho $1 \leq u < v \leq N$ , có một xe tải xuất phát từ ngôi làng thứ $u$, đi qua một hoặc nhiều con đường rồi dừng lại ở ngôi làng thứ $v$. Biết rằng, xe tải luôn chọn  theo tuyến đường qua ít con đường nhất có thể, và khi tới bất kỳ một ngôi làng nào (bao gồm cả hai ngôi làng thứ $u$ và thứ $v$ ), xe tải sẽ thu mua 1 tấn nông sản được sản xuất tại ngôi làng đó. Nhờ mùa màng bội thu, tất cả các ngôi làng đều có đủ nông sản cho mọi xe đi qua thu mua.
- Việc vận chuyển nông sản luôn phát sinh chi phí. Tùy theo đặc tính, chi phí vận chuyển từng loại nông sản có thể khác nhau. Theo tính toán của chính phủ, nếu trong toàn bộ hành trình, một xe tải thu mua được khối lượng nông sản các loại thứ $1,2, \ldots, K$ tương ứng là $W_{1}, W_{2}, \ldots, W_{K}$ tấn, chi phí vận chuyển của xe này là $C_{1} \times W_{1}^{2}+C_{2} \times W_{2}^{2}+\ldots+C_{K} \times W_{K}^{2}$, trong đó $C_{1}, C_{2}, \ldots, C_{K}$ tương ứng là hệ số chi phí vận chuyến cưa $K$ loại nờng sẳn thứ $1,2, \ldots, K$. Chính phủ sẽ tài trợ toàn bộ chi phí vận chuyển, nên cần biết tổng chi phí của tất cả $\frac{N \times(N-1)}{2}$ xe tải này.  
- Ngoài ra, với niềm tin rằng nền nông nghiệp còn phát triển mạnh trong nhiều năm về sau, chính phủ muốn dự trù chi phí vận chuyển nông sản cho những năm tiếp theo. Theo kế hoạch canh tác trong $Q$ năm tiếp theo, vào năm thứ $j$ $(1 \leq j \leq Q)$ ngôi làng thứ $T_{j}$ sẽ chuyển qua sản xuất loại nông sản thứ $B_{j}$, trong khi $N-1$ ngôi làng còn lại sẽ tiếp tục canh tác loại nông sản như năm thứ $j-1$ (năm nay được coi là năm thứ 0). Vơi mỗi năm, chính phủ muốn biết tổng chi phí vận chuyển nông sản nếu tiếp tục bố trí các xe tải thu mua như phương án ở trên. (truy vấn có degenerate)
- **Yêu cầu:** Hãy viết chương trình tính tổng chi phí vận chuyển nông sản của chính phủ trong năm nay và trong $Q$ năm tiếp theo, dựa trên kế hoạch thay đổi canh tác.
### Dữ liệu: Vào từ file văn bản FBUY.INP
- Dòng đầu chứa một số nguyên là phần dư của tổng chi phí vận chuyển nông sản trong năm nay trong phép chia cho 998244353.
- Dòng thứ $j$ trong số $Q$ dòng còn lại chứa một số nguyên là phần dư của tổng chi phí vận chuyển nông sản trong năm thứ $j$ trong phép chia với 998244353.
### Ràng buộc: 
- (1) Có 7.5% số test tương ứng với 7.5% số điểm thỏa mãn: $N \le 3000$ và $Q \le 800$ .
- (2) 12.5% số test khác ứng với 12.5% số điểm thỏa mãn: $N \le 100$ và $Q \le 800$ .
- (3) 10% số test khác ứng với 10% số điểm thỏa mãn: $N \le 2000$ và $Q \le 800$ .
- (4) 15% số test khác ứng với 15% số điểm thỏa mãn: $N \le 5000$ và $Q \le 8000$ .
- (5) 17.5% số test khác ứng với 17.5% số điểm thỏa mãn: Luôn tồn tại một con đường nối ngôi làng thứ $i$ và ngôi làng thứ $[\frac{i}{2}]$, $\forall i = 2,3,....N$ , với $[\frac{i}{2}]$ là số nguyên lớn nhất không vượt quá $\frac{i}{2}$ .
- (6) 22.5% số test khác ứng với 22.5% số điểm thỏa mãn: Luôn tồn tại một con đường nối ngôi làng thứ $i$ và ngôi làng thứ $i-1$ , $\forall i = 2,3,....N$
- (7) 15% số test còn lại ứng với 15% số điểm: Không có ràng buộc gì thêm
### Ví dụ: 



### Giải thích: 
- Trong năm nay, các ngôi làng thứ 1,2,3,4,5 lần lượt sản xuất các loại nông sản thứ 1,1,1,2,3. Có tất cả $\frac{5 \times (5-1)}{2} = 10$ xe tải với các lộ trình vận chuyển và chi phí như sau:



- Tổng chi phí vận chuyển của các xe là: $8+18+11+7+8+5+13+11+23+16=120$ .
- Theo kế hoạch canh tác các năm tiếp theo:
    - Trong năm thứ $1$, các ngôi làng thứ 1,2,3,4,5 sẽ lần lượt sản xuất các loại nông sản thứ 1,3,1,2,3. Số lượng xe và lộ trình di chuyển các xe vẫn giống như ở trên, nhưng tổng chi phí vận chuyển các xe là: $7+13+10+7+7+8+22+10+28+25=137$ .
    - Trong năm thứ $2$, các ngôi làng thứ 1,2,3,4,5 sẽ lần lượt sản xuất các loại nông sản thứ 1,3,2,2,3. Số lượng xe và lộ trình di chuyển các xe vẫn giống như ở trên, nhưng tổng chi phí vận chuyển các xe là: $7+10+10+7+8+8+22+17+25+25=139$ .
  
