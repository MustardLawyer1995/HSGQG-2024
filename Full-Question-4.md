# Câu 4: Sản xuất gỗ 
- WoodPro là một nhà máy nổi tiếng chuyên sản xuất các sản phẩm về gỗ. Do nhu cầu thị trường ngày càng cao, nhà máy quyết định nhập khẩu một dây chuyền thông minh sản xuất hàng loạt những thanh gỗ. Mỗi một lượt sản xuất, dây chuyền sẽ nhận vào $N$ thanh gỗ dạng hình trụ có cùng kích thước đáy. Các thanh gỗ được đánh số từ $1$ đến $N$, thanh gỗ thứ $i$ có độ dài $A_{i}$ xăng-ti-mét. Thứ tự các thanh gỗ đưa vào dây chuyền là $1,2,3...,N$ . Khi dây chuyền bắt đầu hoạt động, các thanh gỗ được xếp nối đuôi nhau trên một băng chuyền, theo đúng thứ tự nhận vào. Băng chuyền này sẽ di chuyển các thanh gỗ đi theo một chiều qua hai công đoạn xử lí, trước tiên là *công đoạn cắt* rồi đến *công đoạn dán*, mà vẫn giữ nguyên thứ tự của các thanh gỗ trên băng chuyền.
    - Ở công đoạn cắt, có một lưỡi cắt được đặt cố định phía trên băng chuyền. Mỗi khi có thanh gỗ di chuyển qua, hệ thống có thể điều khiển lưỡi cắt hạ xuống để cắt thanh gỗ thành hai thanh có tổng độ dài bằng độ dài thanh gỗ trước khi cắt. Sau khi cắt, vị trí của hai thanh gỗ trên băng chuyền vẫn được giữ nguyên. Chi phí cho mỗi lần cắt như vậy là $C$.
    - Ở công đoạn dán, có một máy dán được đặt cố định phía trên băng chuyền. Mỗi khi có hai thanh gỗ kề nhau di chuyển qua, hệ thống có thể điều khiển máy dán hạ xuống để dán hai thanh gỗ này thành thanh gỗ có độ dài bằng tổng độ dài hai thanh gỗ trước khi dán. Sau khi dán, vị trí của hai thanh gỗ trên băng chuyền vẫn được giữ nguyên. Chi phí cho mỗi lần cắt như vậy là $D$.
- Tuấn là một lập trình viên của nhà máy đảm nhận nhiệm vụ lập trình cho hệ thống đối với yêu cầu của mỗi đơn hàng. Do mới nhận được một đơn hàng yêu cầu các thanh gỗ thành phần chỉ gồm loại độ dài $L_{1}$ xăng-ti-mét hoặc độ dài $L_{2}$ xăng-ti-mét, nhà máy giao cho Tuấn lập trình cho hệ thống để sản xuất ra các thanh gỗ thành phẩm như vậy từ $N$ thanh gỗ đầu vào mà không để thừa thanh gỗ nào có độ dài khác $L_{1}$ và $L_{2}$.
- **Yêu cầu**: Biết rằng luôn tồn tại một phương án sản xuất ra các thanh gỗ thành phẩm độ dài $L_{1}$ và $L_{2}$ từ $N$ thanh gỗ đầu vào mà không thừa ra thanh gỗ nào có độ dài khác $L_{1}$ và $L_{2}$, hãy tính tổng chi phí ít nhất có thể dùng cho việc cắt và dán, để dây chuyền sản xuất có thể hoàn thành được đơn hàng.
### Dữ liệu: Vào từ file văn bản WPRO.INP
   - Dòng đầu chứa năm số nguyên $N,L_{1}, L_{2}, C$ và $D$ lần lượt là số lượng thanh gỗ, hai loại độ dài các thanh gỗ thành phẩm đầu ra, chi phí cho một lần cắt và chi phí cho một lần dán: $1 \le N \le {10^4};1 \le {L_1},{L_2} \le {10^9};1 \le C,D \le {10^5}$ .
   - Dòng thứ hai chứa $N$ số nguyên $A_{1}, A_{2},... A_{N}$ là độ dài của $N$ thanh gỗ đầu vào $1 \le {A_i} \le {10^9},\forall i = 1,2,...N$ .
- Dữ liệu bảo đảm luôn có phương án giải quyết theo yêu cầu đề bài.
- Các số trên cùng một dòng cách nhau bởi dấu cách.
### Kết quả: WPRO.OUT
- Ghi ra file văn bản WPRO.OUT một số nguyên là tổng chi phí dùng cho việc cắt và dán tìm được
### Ví dụ: 

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/326f8ef3-b38a-42e2-9a11-d65359075872)

![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/9b167569-358f-4788-b1e6-4af3a6cc4ab1)

### Ràng buộc:  
- (1) Có 16% số test ứng với 16% số điểm thỏa mãn: $L_{1}=L_{2}$ .
- (2) 16% số test khác ứng với 16% số điểm thỏa mãn: $\sum _ {i \to N} A_{i} \le 20$ .
- (3) 16% số test khác ứng với 16% số điểm thỏa mãn: $N,L_{1},L_{2} \le 100$ và $A_{i} \le 100, \forall i = 1,2,...N$ 
- (4) 16% số test khác ứng với 16% số điểm thỏa mãn: $A_{i} \le 2024, \forall i = 1,2,...N$
- (5) 12% số test khác ứng với 12% số điểm thỏa mãn: $L_{1},L_{2} \le 2024$
- (6) 12% số test khác ứng với 12% số điểm thỏa mãn: $L_{1} \le 2024$
- (7) 12% số test còn lại ứng với 12% số điểm: Không có ràng buộc gì thêm. 









