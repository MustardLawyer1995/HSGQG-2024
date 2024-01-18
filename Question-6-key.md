# Câu 6: Bài tập đêm Giáng Sinh
## Tóm tắt đề bài: 
- Cho dãy số $C[1], C[2], ..., C[n]$ thoả mãn $C[i]$ khác $C[i+1]$ với mọi $i$.
- Có $Q$ truy vấn dạng $L$, $R$, $X$, $Y$
- Xét các cách chia dãy $C[L..R]$ làm các đoạn liên tiếp không có phần tử lặp
- Tìm cách chia có thứ tự từ điển lớn thứ X và lớn thứ Y
- In ra tiền tố chung dài nhất của hai dãy
    - $n,q \le 2e5;{\rm{ }}X,Y \le 1e17$. 
- Thứ tự từ điển:
    - Sắp xếp theo độ dài đoạn đầu tiên giảm dần
    - Cùng độ dài đoạn đầu tiên --> sắp xếp theo độ dài đoạn thứ hai giảm dần
    - Cùng độ dài đoạn đầu tiên và thứ hai --> sắp xếp theo độ dài đoạn thứ ba giảm dần...
## Phân tích ràng buộc bài toán

![image](https://github.com/MustardLawyer1995/HSGQG-2024/assets/156400720/fb9c4411-09e6-4bd0-9ad8-ab51ef27b057)

## Phân tích từng Subtask 
### Subtask 1: $n \le 12$ và $q \le 1024$
- Duyệt vét cạn mọi phương án chia đoạn. 
- Dãy $C[L], C[L + 1], ..., C[R]$ có tối đa $2^{R - L}$ cách chia làm các đoạn con liên tiếp
- Độ phức tạp: $O(2^n \times Q)$
### Subtask 2: $X=Y=1$
- Yêu cầu: Tìm số đoạn trong cách chia đoạn có thứ tự từ điển lớn nhất
- Áp dụng thuật toán tham lam, ta chọn đoạn có độ dài dài nhất có thể.
- Gọi $range[l] =$ giá trị r lớn nhất để đoạn $[l..r]$ có các phần tử đôi một phân biệt. Tính mảng range bằng phương pháp hai con trỏ. Đặt $next[l] = range[l] + 1$, khi đó đoạn $[L..R]$ sẽ được chia làm các đoạn như sau:
    - Gọi $i = L, j = next[i], k = next[j], t = next[k]$.
	  - Các đoạn được chia: $[i .. j - 1], [j .. k - 1], [k .. t - 1], ... $.
- Số đoạn trong cách chia chính là số bước của quá trình nhảy
    - $L -> next[L] -> next[next[L]] -> next[next[next[L]]] -> ...$ cho tới khi dừng lại tại vị trí $> R$.
- Sử dụng bảng thưa: $next[i, j]$ là vị trí đạt được nếu từ $i$ nhảy $2^j$ bước:
    - $next[i, 0] = next[i]; next[i, j] = next[next[i, j - 1], j - 1]$.
### Subtask 3: $L=1,R=n$ và $X,Y \le 1e5$
- Dùng thuật toán backtrack sinh ra 1e5 cách chia đoạn của dãy $C[1], C[2], ..., C[n]$ có thứ tự từ điển lớn nhất.
- Sử dụng TRIE để lưu lại 1e5 cách này.
- Dễ thấy cách thứ 1 và cách thứ 1e5 chỉ lệch nhau ở tối đa 26 phần tử cuối cùng -> Số nút của cây TRIE không quá $n + 1e5 \times 26$.
- Tiền tố chung dài nhất chính là LCA trên cây TRIE.
```cpp
int cnt = 0;
void backtrack(vector<int> &lengths, int cur) {
	if (cur > n) {
		++cnt;
		// ghi nhận lengths là vector thể hiện cách phân đoạn thứ cnt
		return;
	}
	for (i : range[cur] -> cur) {
		lengths.push_back(i - last + 1);
		backtrack(lengths, i + 1);
		lengths.pop_back();
	}
}
vector<int> v;
backtrack(v, 1);
```
```cpp
struct Node {
	Node *parent;
	int high;
	Node(Node *par = nullptr) {
		parent = par;
		high = parent == nullptr ? 0 : parent->high + 1;
	}
};
Node *leaves[100100];
int lca(Node *p, Node *q) {
	while (p->high > q->high) p = p->parent;
	while (q->high > p->high) q = q->parent;
	while (p != q) { p = p->parent; q = q->parent; }
	return p->high;
}
```
```cpp
int cnt = 0;
void backtrack(Node *p, int cur) {
	if (cur > n) {
		leaves[++cnt] = p;
		return;
	}
	for (i : range[cur] -> cur) backtrack(new Node(p), i + 1);
}
backtrack(new Node(), 1);
```
### Subtask 4: $n \le 2000$ và $q \le 20000$
- Tính trước mảng $cnt[l, r] =$ số cách phân đoạn dãy $[l, r]$.
- Coi $cnt[r + 1, r] = 1$. Khi đó $cnt[l, r] =$ tổng $cnt[i + 1, r]$ với $l \le i \le min(range[l], r)$.
- Sau đó sinh ra dãy có thứ tự từ điển thứ x bằng thuật toán thứ tự từ điển thông thường.
```cpp
void getKth(int l, int r, long long k, vector<int> &res) {
	int cur = l;
	while (cur <= r) {
		for (i : min(range[cur], r) -> cur) {
			if (cnt[i + 1, r] >= k) {
				res.push_back(i - cur + 1);
				cur = i + 1;
				break;
			} else k -= cnt[i + 1, r];
		}
	}
}
```
### Subtask 5: Không có ràng buộc gì thêm
- Do $C[i]$ khác $C[i + 1]$ nên $range[i] > i$ với mọi $i$.
- Do đó $F[l, r] \ge F[l + 1, r] + F[l + 2, r]$ tức khi đó với mọi $r$, dãy $F[r, r], F[r - 1, r], F[r - 2, r], ..., F[1, r]$ tăng nhanh hơn dãy Fibonacci.
- Do $Fib[85] > 1e17$ nên suy ra $F[l, r] > 1e17$ với mọi đoạn có độ dài lớn hơn 85 nên ta chỉ cần tính $F[l, r]$ với các cặp $r - l \le 85$
- Với dãy có thứ tự từ điển thứ $X, Y \le 1e17$:
   - Luôn chọn đoạn dài nhất có thể cho tới khi phần còn lại có dưới 85 phần tử.
   - Ta dùng bảng thưa để tìm nhanh đoạn này, phần này chắc chắn thuộc LCP.
   - 85 phần tử cuối ta sinh ra bằng thuật toán thứ tự từ điển thông thường.









