# Câu 1: Ba đường truyền điện (7 điểm)
- Quốc gia Alpha có một trang trại điện gió được quy hoạch bởi một bảng vuông $N$ hàng và $N$ cột. Các hàng được đánh số từ 1 tới $N$ từ trên xuống dưới, các cột được đánh số tữ 1 tới $N$ từ i sang phải. Trang trại có $M$ trạm sản xuất điện gió được đánh số từ 1 tới $M$. Trạm thứ $i$ $(1 \leq i \leq M)$ được đặt tại ô thuộc hàng $R_{i}$, cột $C_{i}$ và có công suất sản xuất là $W_{i}$ oát. Chủ trang trại mới ký hợp đồng cung cấp điện cho đối tác. Trang trại sẽ phải lắp ba đường truyển điện, mỗi đường truyền đi qua một hàng hoặc một cột trong bảng. Các đường truyền có thể cắt nhau nhưng không được trùng nhau. Tổng công suất cung cấp cho đối tác là tổng công suất của các trạm điện nằm  ít nhất một trong ba đường truyền. Trang trại cần tìm ra cách lắp đặt ba đường truyền để tổng công suất cung cấp là lớn nhất có thể.  
- Ngoài ra, công ty có $Q$ phương án điều chỉnh. Phưong án điều chỉnh thứ $j$ $(1 \leq j \leq Q)$ là tăng công suất của trạm $T_{j}$ thêm một lượng $D_{j}$ oát và giữ nguyên công suất $W_{i}$ oát như hiện trạng ban đẩu của mọi trạm $i$ khác $T_{j}$. Lưu ý, các phương án là độc lập, nghĩa là các phương án đều chỉ áp dụng lên hiện trạng ban đầu của trang trại. (các query là non degenerate)  
- **Yêu cầu**: Hãy đưa ra tổng công suất lớn nhất có thể khi lắp ba đường truyền với hiện trạng ban đầu của trang trại và trong $Q$ phương án điều chỉnh.  
### Dữ liệu: Vào từ file văn bản THREE.INP:  
- Dòng đầu ghi một số nguyên dương $\mathcal{T}$ là số lượng trường hợp test  (multi test)  
- Mỗi nhóm dòng trong số $\mathcal{T}$ nhóm dòng tiếp theo mô tả một trường hợp test có cấu trúc như sau:  
   - Dòng thứ nhất chứa ba số nguyên $N, M$ và $Q$ điện và số lượng phương án điều chỉnh $\left(3 \leq N \leq 10^{9} ; 3 \leq M \leq 10^{5} ; 1 \leq Q \leq 10^{5}\right)$.  
   - Dòng thứ $i$ trong số $M$ dòng tiếp theo chứa ba số nguyên $R_{i}, C_{i}$ và $W_{i}$ lần lượt là vị trí hàng, vị trí cột và công suất của trạm điện thứ $i$. (1ữ liệu bảo đảm không có hai trạm nào đặt tại cùng một ô $\left(1 \leq R_{i}, C_{i} \leq N ; 1 \leq W_{i} \leq 10^{9}\right)$ 
   - Dòng thứ $j$ trong số $Q$ dòng tiếp theo chứa hai số nguyên $T_{j}$ và $D_{j}$ thể hiện phương án điḕu chỉnh tăng công suất thêm $D_{j}$ oát cho trạm điện thứ $T_{j}\left(1 \leq T_{j} \leq M ;\left(\leq D_{j} \leq 10^{18}\right)\right.$
   - Gọi $\Sigma_{M}$ và $\Sigma_{Q}$ tương ứng là tổng của tất cả các giá trị $M$ và $Q$ trong tất cả $\mathcal{T}$ trường hợp test. Dữ liệu bảo đảm $1 \leq \Sigma M, \Sigma Q \leq 2 \times 10^{5}$.  
   - Các số trên cùng một dòng cách nhau bởi dấu cách.
### Kết quả: Ghi ra file văn bản THREE.OUT:  
- Gồm $\mathcal{T}$ nhóm dòng, mỗi nhóm dòng là kết quả của trường hợp test tương ứng có cấu trúc sau:  
   - Dòng thứ nhất ghi ra một số nguyên dương là tổng công suất lớn nhất tìm được với hiện trạng trang trại ban đầu.  
   - Dòng thứ $j$ trong số $Q$ dòng tiếp theo ghi ra tổng công suất lớn nhất tìm được với phương án điều chỉnh thứ $j$.
### Ví dụ:
<table style="border-collapse: collapse; margin: auto;">
  <tr>
    <td style="border: 1px solid black; text-align: center;">
      <div style="text-align: center;">
        <!-- First 5x5 Nested Table -->
        <table style="border-collapse: collapse; margin: auto;">
          <!-- Each row -->
          <tr><td style="border: 1px solid black; width: 30px; height: 30px;">1</td>
              <td style="border: 1px solid black; width: 30px; height: 30px;"></td>
              <td style="border: 1px solid black; width: 30px; height: 30px;"></td>
              <td style="border: 1px solid black; width: 30px; height: 30px;"></td>
              <td style="border: 1px solid black; width: 30px; height: 30px;">5</td></tr>
          <tr><!-- ... --></tr>
          <!-- Repeat <tr> 5 times entirely with <td>s to make a 5x5 table... -->
        </table>
        <!-- Space between the two tables -->
        <div style="height: 10px;"></div>
        <!-- Second 5x5 Nested Table -->
        <table style="border-collapse: collapse; margin: auto;">
          <!-- Repeat the structure of the first 5x5 nested table -->
          <tr><td style="border: 1px solid black; width: 30px; height: 30px;"></td> <!-- Repeat <td> 5 times... --></tr>
          <tr><!-- ... --></tr>
          <!-- Repeat <tr> 5 times entirely with <td>s to make a 5x5 table... -->
        </table>
      </div>
    </td>
  </tr>
</table>
### Ràng buộc: 
   - (1) Có $20 \%$ số test ứng với $20 \%$ số điểm thỏa mãn: $N, M, Q \leq 40$ và $\mathcal{T}=1$.  
   - (2) $20 \%$ số test khác ứng với $20 \%$ số điểm thỏa mān: $N, M, Q \leq 100$ và $\mathcal{T}=1$.  
   - (3) $20 \%$ số test khác ứng với $20 \%$ số điểm thỏa mãn: $N, M, Q \leq 500$ và $\mathcal{T}=1$.  
   - (4) $20 \%$ số test khác ứng với $20 \%$ số điểm thỏa mãn: $M, Q \leq 1000$ và $\Sigma M, \Sigma Q \leq 2000$.  
   - (5) $10 \%$ số test khác ứng với $10 \%$ số điểm thỏa mãn: $M \leq 1000$ và $\Sigma M \leq 2000$.  
   - (6) $10 \%$ số test còn lại ứng với $10 \%$ số điểm: Không có ràng buộc gì thêm.













