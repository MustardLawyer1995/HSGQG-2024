
# Câu 1: Ba đường truyền điện
Tóm tắt đề bài: Cho một bảng $N \times N$ và $M$ điểm trên bảng, điểm thứ $i$ nằm trên hàng $[A][R_i][C_i]$ có trọng số $W_i$. Cho $Q$ truy vấn độc lập, truy vấn thứ $j$ sẽ tăng giá trị của điểm thứ $T_j$ trên $D_j$. Sau khi thực hiện mỗi truy vấn, hãy chọn ra 3 hàng và cột, sao cho tổng trọng số của các ô được chọn là tốt nhất 
Note: Truy vấn độc lập là các truy vấn chỉ áp dụng lên hiện trạng ban đầu của bảng
## Phân tích ràng buộc bài toán
- Có $T$ test, với mỗi test: $3 \le N \le 109,3 \le M \le 105,1 \le Q \le 105,1 \le {W_i} \le 109,1 \le {D_j} \le {10^{18}}\$
- Dữ liệu đảm bảo $1 \le \sum M ,\sum Q  \le 2 \times {10^5}\$
![Capture](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/5e6ca5dd-5936-4388-8c73-e24ff1d755c2)
## Phân tích từng subtask
### Subtask 1: $M,N,Q \le 40$ và $T=1$
- Ở subtask này, chúng ta có thể duyệt thủ công bằng tay ở mọi trường hợp (hàng/cột) có thể xảy ra cho mỗi truy vấn. 
- Độ phức tạp: $O(Q \times N^3)$
### Subtask 2: $M,N,Q \le 100$ và $T=1$
- Ở subtask này, chúng ta đưa ra một phán xét nhỏ: nếu tăng ô $A[i][j]$ thì khi đó đáp án của truy vấn hoặc không thay đổi, hoặc phải chứa hàng $i$, cột $j$. Lúc này ta có thể duyệt thủ công bằng tay ở 2 hàng/cột còn lại
- Độ phức tạp: $O(Q \times N^2)$
### Subtask 3: $M,N,Q \le 100$ và $T=1$
- Note: $\sum_{col}[j]=$ sum_col $[j]$
- Khi tìm cấu hình tốt nhất cho bảng, ta có 4 trường hợp: 3 hàng, 3 cột, 1 hàng + 2 cột, 1 cột + 2 hàng. Không mất tính tổng quát, chúng ta sẽ xét 2 trường hợp: 3 hàng và 1 hàng + 2 cột.
- Với trường hợp 3 hàng, ta chỉ cần đơn giản chọn ra 3 hàng có tổng lớn nhất.  
- Với trường hợp 1 hàng + 2 cột: đặt $\sum_{col}[j]$ là tổng các số trong cột thứ $j$. Ta sẽ lưu tất cả các giá trị $\sum_{col}[]$ vào một set/multiset.  
- Nếu ta chọn hàng thứ $i$, với mỗi giá trị $a[i][j]$, ta sẽ cập nhật $\sum_{col}[j] -= a[i][j]$ vào set. Sau đó, ta sẽ chọn ra 2 cột có tổng lớn nhất.  
- Dễ thấy set chỉ bị cập nhật tối đa $M$ lần, vì vậy độ phức tạp của mỗi truy vấn sẽ là $O(M \log N)$.
- Độ phức tạp: $O\left( {Q \times N\log N} \right)\$
### Subtask 4: $M,Q \le 1000$ và $\sum M ,\sum Q \le 2000$
- Ta có thể áp dụng thuật toán tương tự subtask 3 với một cải tiến nhỏ: ta chỉ cần lưu tối đa $M$ giá trị sum_col $[j]$ trong set thay vì lưu toàn bộ $N$ cột. 
- Độ phức tạp: $O\left( {Q \times M\log M} \right)\$
### Subtask 5: $M \le 1000$ và $\sum M \le 2000$
- Ta chỉ cần cải tiến “nhẹ” từ subtask 4: thay vì xử lý từng truy vấn, ta lưu các truy vấn lại và xử lý offline cùng lúc các truy vấn thay đổi hàng thứ $i$.
- Độ phức tạp: $O\left( {Q + {M^2}\log M} \right)\$
### Subtask 6: Không giới hạn gì thêm
- Ở subtask này, ta sẽ sử dụng lại ý tưởng của subtask 2: khi cập nhật ô $A[i][j] += D$, đáp án hoặc không thay đổi, hoặc phải chứa hàng $i$/cột $j$. 
- Ta có thể chia thành 6 trường hợp: 3 hàng, 3 cột, hàng $i$ + 2 cột, cột $j$ + 2 hàng, hàng $i$ + 1 hàng + 1 cột, cột $j$ + 1 hàng + 1 cột. Tương tự subtask 3, không mất tính tổng quát, ta chỉ quan tâm 3 trường hợp chính:
- Trước hết chọn 3 hàng: ta chỉ cần cập nhật lại sum_row[] và chọn ra 3 tổng lớn nhất.
```cpp 
long long choose_three_rows(int i, int D) {
  sum_row_set.erase({sum_row[i], i});
  sum_row_set.insert({sum_row[i] + D, i});
  auto it = sum_row_set.begin();
  long long ret = (*it++).first + (*it++).first + (*it).first;
  sum_row_set.erase({sum_row[i] + D, i});
  sum_row_set.insert({sum_row[i], i});
  return ret;
}
```
- Chọn hàng $i$ + 2 cột khác: tương tự subtask 3, ta chỉ cần cập nhật lại set sum_col[] và chọn ra 2 tổng lớn nhất. Để tránh cập nhật nhiều lần, ta sẽ xử lý các truy vấn của hàng $i$ cùng lúc.
```cpp
void choose_two_cols(int i) {
  for (auto [j, v] : row[i]) { // a[i][j] = v
    sum_col_set.erase({sum_col[j], j});
    sum_col_set.insert({sum_col[j] - v, j});
  }
  auto it = sum_col_set.begin();
  long long ret = sum_row[i] + (*it++).first + (*it).first;

  for (auto [id, j, D] : query_row[i]) {
    // the id-th query is a[i][j] += D
    ans[id] = max(ans[id], ret + D);
  }
  // ... restore the sum_col_set
}
```
- Chọn hàng $i$ + 1 hàng + 1 cột:
  - Ở trường hợp này, ta sẽ tính mảng best_for_col[j] = {best_val, best_row}, thể hiện hàng có tổng lớn nhất khi ta cố định cột $j$. Lưu các tổng sum_col[j] + best_val vào một set/multiset, ta sẽ chọn ra được đáp án tối ưu nhất cho hàng $i$.
  - Tuy nhiên, làm sao để xử lý trường hợp best_row = i ? Ta chỉ cần lưu thêm một mảng second_best_for_col[i], và cập nhật lại set. Dễ thấy ta chỉ lưu tối đa $M$ cột, vì vậy multiset sẽ chỉ bị cập nhật lại tối đa $M$ lần.
  - Tương tự trường hợp trước, ta cũng sẽ xử lý các truy vấn của hàng $i$ cùng lúc. 
- Độ phức tạp: $O\left( {Q \times M\log M} \right)\$
```cpp
void calc_best() {
  for (int j : list_col) {
    for (auto [i, v] : col[j]) { // a[i][j] = v;
      sum_row_set.erase({sum_row[i], i});
      sum_row_set.insert({sum_row[i] - v, i});
    }
    auto it = sum_row_set.begin();
    best_for_col[j] = {(*it).first + sum_col[j], (*it).second};
    best_for_col_set.insert({best_for_col[j].first, j});
    best_row[(*it).second].push_back(j);
    second_best_for_col[j] = *(++it).first + sum_col[j];
    // ... restore the sum_row_set
  }
}
```
```cpp
void choose_one_row_and_one_col(int i) {
  for (auto j : best_row[i]) {
    best_for_col_set.erase({best_for_col[j].first, j});
    best_for_col_set.erase({second_best_for_col[j], j});
  }
  for (auto [j, v] : row[i]) { // a[i][j] = v
    if (best_for_col[j].second != i) {
      best_for_col_set.erase({best_for_col[j].first, j});
      best_for_col_set.insert({best_for_col[j].first - v, j});
    } else {
      best_for_col_set.erase({second_best_for_col[j], j});
      best_for_col_set.erase({second_best_for_col[j] - v, j});
    }
  }
  long long ret = sum_row[i] + (*best_for_col_set.begin()).first;
  for (auto [id, j, D] : query_row[i]) {
    ans[id] = max(ans[id], ret + D);
  }
  // .... (restore the best_for_col_set)
}
```
















