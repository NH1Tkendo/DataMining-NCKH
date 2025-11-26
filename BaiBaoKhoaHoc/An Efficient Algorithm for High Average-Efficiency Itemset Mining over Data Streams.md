
Đóng góp của bài báo này:
* Thuật toán khai thác mẫu tiện ích trung bình cao cho dữ liệu luồng
* Cấu trúc dữ liệu TWAE-List -> kết hợp thông tin ở mức độ giao dịch và mức độ cửa sổ
* 2 cận trên chặt chẽ hơn để làm giảm ứng cử viên
	* Cận trên relative maximum average-efficiency upper bound (MEAUB) -> Ước tính hiệu quả trung bình cao nhất có thể đạt được bằng cách xem xét đồng thời tiện ích và chi phí đầu tư của một tập mục và các mở rộng của nó
	* Cận trên estimated average-efficiency upper bound (EAEUB) -> bỏ các itemsets không đạt chuẩn trong giai đoạn tái cấu trúc
* Chiến thuật efficient transaction pruning (ETP) -> Cắt tỉa giao dịch hiệu quả nhằm tốc độ cập nhật cửa sổ trong dữ liệu luồng. Chiến lược này giảm đáng kể chi phí tính toán khi duy trì cấu trúc danh sách trên các cửa sổ trượt và đảm bảo tính kịp thời của việc khai thác tập mục có hiệu quả trung bình cao.
* HAEIM_Stream -> Thuật toán khai thác tiện ích có hiệu quả trung bình cao trong dữ liệu luồng được đề xuất dựa trên TWAE-List, MAEUB, EAEUB, ETP

Ghi chú:
- 1 phần (batchs) = 2 giao dịch
- 1 cửa sổ trượt = 2 phần = 4 giao dịch

Khi cửa sổ trượt di chuyển, nó bỏ 1 batchs cũ nhất ra khỏi nó và thêm 1 batchs mới nhất vào

![[Pasted image 20251125135800.png]]

![[Pasted image 20251125135819.png]]
## Phần 3:

### **Định nghĩa 1**: Nội tiện ích (Internal Utility). 
Nội tiện ích(Số lượng) của một item $i_l$ trong một giao dịch $T_j$ Được định nghĩa là $qu(i, T_c)$
* Ví dụ: $qu(c, T_1)$ = 1

### **Định nghĩa 2**: Ngoại tiện ích (External Utility). 
Với mỗi item $i_l \in I$, ngoại tiện ích của nó là một số dương được định nghĩa là $eu(i_l)$
* Ví dụ: $eu(c) = 5$ 

### **Định nghĩa 3**: Tiện ích (Utility)
* Tiện ích của một item: $u(i_l, T_j) = eu(i_l) \times qu(i_l, T_j)$ 
* Tiện ích của một itemsets: $u(X, T_i) = \sum_{i \in X} u(i, T_i)$

### **Định nghĩa 4**: Tiện ích còn lại (Remaining Utility) 
là các item còn lại sau item đang được xét
* Ví dụ: $T_1 / {ac} = {d,f}$, $ru({a,b}, T_1) = u({d,f}, T_1) = 2 \times 2 + 1 \times 2 = 6$

### **Định nghĩa 5**: Mức độ đầu tư (Investment) 
* Mỗi item $i_l$ có mức độ đầu tư $cu(i_l)$ 
* Trong một giao dịch $T_j$, mức độ đầu tư được ký hiệu là $inv(i_l, T_j) = cu (i_l) qu(i_l, T_j)$ 
* Tổng mức độ giao dịch trong một luồng $inv(i_l) = \sum_{T_j \in DS} inv(i_l, T_j)$ 

Ví dụ: $qu(e, T_2)$ và $cu(e) = 13$ => $inv(e, T_2) = 2 \times 13 = 26$ => $inv(e) = inv(e, T_2) + .... + inv(e,T_8) = 26 + 13 +13 + 13 +26 = 91$ 
![[Pasted image 20251125140939.png]]

### **Định nghĩa 6**: Hiệu suất (Efficiency) 
* Hiệu suất của một itemset $X$ trong một batch $B_r$ được định nghĩa là $E(X, B_r) = \frac{u(X, B_r)}{inv(X)}$ 
* Hiệu suất của một itemset $X$ trong một cửa sổ trượt $W_n$ được định nghĩa là $E(X, W_n) = \frac{u(X, W_n)}{inv(X)}$  
Ví dụ: 
* Hiệu suất của itemset {ac} trong batch $B_1$ 
$$E(\{ac\}, B_1) = \frac{u(\{ac\}, T_1) + u(\{ac\}, T_2)}{inv(ac)} = \frac{9+14}{96+72} = 0.137$$
* Hiệu suất của {ac} trong cửa sổ trượt $W_1$ 
$$E(\{ac\}, W_1) = \frac{u(\{ac\}, B_1) + u(\{ac\}, B_2)}{inv(ac)} = \frac{23+29}{96+72} = 0.31$$
### **Định nghĩa 7**: Hiệu suất trung bình (Average-eficiency)

Hiệu suất trung bình của itemset X trong batch $B_r$ được mô tả là:
$$AE(X, B_c) = \frac{u(X, B_r)}{inv(X) \times |X|}$$
Ví dụ: Hiệu suất trung bình của itemset {ac} trong batch $B_1$ 
$$AE(\{ac\}, B_1) = \frac{u(\{ac\}, T_1) + u(\{ac\}, T_2)}{inv(ac) \times |ac|} = \frac{9+14}{(96+72) \times 2} = 0.068$$
### Định nghĩa 8: Tiện ích tối đa (Maximum utility)

Tiện ích tối đa của một giao dịch $T_j$ được định nghĩa là $$mu(T_j) = \max\{u(i_l, T_j) \mid i_l \in T_j\}$$
Ví dụ: Tiện ích tối đa của $T_2$ là $mu(T_2) = \max\{u(i_l, T_2) \mid i_l \in T_2\} = 12$

### Định nghĩa 9: Chặn trên tiện ích trung bình (Average-efficiency upper bound - AEUB) 
* Trong một giao dịch: $AEUB(X, T_j) = \frac{mu(T_j)}{inv(X)}$
*  Trong một batch: $AEUB(X, B_r) = \sum_{T_j \in B_r, X \subseteq T_j} AEUB(X, T_j)$
*  Trong một cửa sổ trượt: $AEUB(X, W_n) = \sum_{T_j \in W_n, X \subseteq T_j} AEUB(X, T_j)$
Ví dụ
* $AEUB(a, T_1) = \frac{5}{96} = 0.052$
* $AEUB(a, B_1) = AEUB(a, T_1) + AEUB(a, T_2) = 0.052 + 0.125 = 0.177$

### Định nghĩa 10: Hiệu suất trung bình cao của itemset (HAEI)

Gọi $minae$ là ngưỡng hiệu suất trung bình tối thiểu. Một itemset X được gọi là một itemset hiệu suất trung bình cao trong một cửa sổ trượt $W_n$ nếu hiệu suất trung bình thỏa mãn $AE(X, W_n) \geq minae$

Ví dụ: với $minae = 0.1$  với itemset {a,c} trong cửa sổ $W_1$ => $AE({a,c},W_1) = 0.155 \geq minae = 0.1$ => {a,c} là HAEI của $W_1$

#### Bổ đề 1: Hiệu suất trung bình (AE) của một itemset X trong cửa sổ $W_n$ luôn bé hơn hoặc bằng so với chặn trên hiệu suất trung bình của nó (AEUB)

#### Bổ đề 2: Với một itemset X và bất kì siêu tập hợp nào của nó thì 
$$AEUB(X, W_n) \geq AEUB(X^S, W_n)$$

### Định nghĩa 11 (Tiện ích tiền tố) 
Với một itemset X và các mở rộng của nó $E(X) \mid y \in E(X)$, tiền tố tiện ích của itemset được mở rộng $X_y$ trong giao dịch $T_j$ được tính là $pu(X_y, T_j) = u(X, T_j)$  

E(X) là tập các item có thể thêm vào X để mở rộng hơn

Ví dụ: $X = {a,d}$ và $E(X) = {e,f}$  trong giao dịch $T_2$ -> $X_y = \{a,d,e\}$ là $pu(\{a, d, e\}) = u(\{a, d\}, T_2) = 14$

### Định nghĩa 12 (Mức độ đầu tư tiền tố)
Được định nghĩa là $pi(X_y) = inv(X)$

Ví dụ: $Xy = \{b, c, d\}$ is $pi(\{b, c, d\}) = inv(\{b, c\}) = 123$

#### Problem Statement
Cho một luồng dữ liệu DS, minae, winSize, và batchSize, nhiệm vụ của khai thác các itemset hiệu quả trung bình cao là khám phá ra tất cả các itemsets trong cùng một cửa sổ trượt đáp ứng được hiệu quả trung bình hoặc có giá trị lớn hơn minae

## Phần 4: Cấu trúc dữ liệu và thuật toán chính

### 4.1 Cận trên MAEUB

MAEUB ước tính giá trị hiệu suất trung bình cao nhất mà một item có thể đạt được bằng cách kết hợp các items đang được xét duyệt trong khi xem xét tiện ích và mức độ đầu tư của chúng

#### Định nghĩa 13: Cận trên hiệu suất trung bình tối đa (MAEUB)

$T_r$ là danh sách các item trong $T_j$ nhưng được sắp xếp theo thứ tự tiện ích giảm dần

$$ae_n = \frac{u(i_l, T_j) + \sum_{k=1}^{n} u(i_k, T_r)}{(1 + n) \times (inv(i_l) + \sum_{k=1}^{n} inv(i_k))}$$
$$ae_{\max} \leftarrow \max(ae_{\max}, ae_n), (u(i_{n+1}, T_r) < \frac{u(i_l, T_j) + \sum_{k=1}^{n} u(i_k, T_r)}{1 + n})$$
$$MAEUB(i_l, T_j) = ae_{\max}$$
Ví dụ: Tính MAEUB của item a trong $T_1$
* Ta có $T_r = \{(c, 5), (a, 4), (d, 4), (f, 2)\}$
$$ae_0 = \frac{u(a, T_1)}{inv(a) \times 1} = \frac{4}{96} = 0.042$$

Vì $u(i_1,T_r) = 5 > \frac{u(a,T_1)}{1} = 4$, kết hợp a với $i_1$ có thể cho ra hiệu suất trung bình cao hơn. Từ đó tính $ae_1$ $$ae_1 = \frac{u(a, T_1) + u(i_1, T_r)}{(inv(a) + inv(i_1)) \times 2} = \frac{4+5}{(96+72) \times 2} = 0.027$$
Vì $ae_1 < ae_0$ , giá trị lớn nhất vẫn là $ae_0$ . Tiếp theo, kiểm tra các kết hợp tiếp theo có thể làm tăng giá trị hiệu suất trung bình, Vì $$u(i_2, T_1) = 4 < \frac{u(a, T_1) + u(i_1, T_r)}{2} = 4.5$$
Nên các mở rộng về sau không còn hứa hẹn nữa. Do đó, $MAEUB(a,T_1) = ae_0 = 0.042$
#### Bổ đề 3: 
Giá trị MAEUB của $i_l$ trong giao dịch $T_j$ là giá trị cận trên hiệu suất trung bình tối đa có thể đạt được bởi $i_l$ và bất cứ siêu tập hợp nào của nó trong $T_j$ 

#### Bổ đề 4:
MAEUB cung cấp một cận trên chặt chẽ hơn so với AEUB => $MAEUB(i_l,T_j) \leq AEUB(i_l, T_j)$ 

#### Bổ đề 5:
$AE(i_l,T_j)$ luôn luôn bé hơn hoặc bằng $MAEUB(i_l,T_j)$ 

#### Định nghĩa 14: MAEUB trong Batch và Window
$$MAEUB(X, B_r) = \sum_{T_j \in B_r, X \subseteq T_j} MAEUB(X, T_j)$$
![[Pasted image 20251126131036.png]]

#### Thuộc tính 2: Cắt tỉa MAEUB

Trong một cửa sổ trượt $W_n$, nếu một itemset X có $MAEUB(X,W_n) < minae$ thì mọi siêu tập hợp của nó đều không thể được xem là tập hợp hiệu suất trung bình cao

### 4.1 Cận trên ước tính hiệu suất trung bình

Phần này giới thiệu mô hình ước tính hiệu suất trung bình tối đa còn lại -> đầu ra là chặn trên cho các itemset có tiềm năng trở thành hiệu suất trung bình => Cắt tỉa các mẫu không có tiềm năng một cách nhanh chóng và tránh việc nối danh sách không cần thiết

#### Định nghĩa 15: Mức độ đầu tư tối thiểu còn lại (Minimum Remaining Investment)
$$minInv(X, T_j) = \min\{inv(i_1), inv(i_2), \ldots, inv(i_l)\}, where i_l \in T_j / X$$
Ví dụ: Xét $T_2$ với itemset X = {a,c} với $T_2$ được sắp xếp tăng dần theo bảng chữ cái
$$minInv(X, T_2) = \min\{inv(d), inv(e), inv(f)\} = \min\{72, 91, 50\} = 50$$
#### Định nghĩa 16: Ước tính cận trên hiệu suất trung bình (Estimated average-efficiency upper bound, EAEUB)
$$EAEUB(X, T_j) = \begin{cases} \frac{u(X, T_j) + ru(X, T_j)}{(inv(X) + minInv(X, T_j)) \times (|X|+1)}, & ru(X, T_j) > 0 \\ 0, & ru(X, T_j) = 0 \end{cases}$$
Trong môt batch và window
$$EAEUB(X, B_r) = \sum_{T_j \in B_r} EAEUB(X, T_j)$$
$$EAEUB(X, W_n) = \sum_{B_r \in W_n} EAEUB(X, B_r)$$
Ví dụ: Xét X = {a,c} trong giao dịch $T_1$ (Các item được sắp xếp theo bảng chữ cái). Ta có
$$minInv(\{a, c\}, T_1) = \min\{inv(d), inv(f)\} = \min\{162, 50\} = 50$$
$$EAEUB(\{a, c\}, T_1) = \frac{u(\{a,c\}, T_1) + ru(\{a,c\}, T_1)}{(inv(\{a,c\}) + minInv(\{a,c\}, T_1)) \times (|\{a,c\}|+1)} = \frac{9+6}{(168+50) \times 3} = 0.023$$
Giá trị của EAEUB trong $W_1$ là
$$EAEUB(\{a, c\}, W_1) = \sum_{T_j \in W_1} EAEUB(\{a, c\}, T_j) = 0.023 + 0.067 + 0.042 = 0.132$$

#### Bổ đề 6: Bất kì item X nào và các mở rộng của nó $X^S$ -> $EAEUB(X^S,W_n) \leq EAEUB(X,W_n)$ 

#### Thuộc tính 3: Cắt tỉa EAEUB
Trong cửa sổ $W_n$, nếu cận trên ước tính hiệu suất trung bình của một itemset X thỏa $EAEUB(X,W_n) \le minae$  vậy tất cả siêu tập hợp của nó không là HAEIs

### 4.3 Khởi tạo TWAE-List
![[Pasted image 20251126142529.png]]

#### Định nghĩa 17: Tiện ích của các batch cũ (Utility of Old Batches)
Trong cửa sổ $W_n$, tiện ích của itemset X của các batch hết hạn được định nghĩa là 
$$OldU(X, W_n) = \sum_{T_j \in OldBatch \wedge X \subseteq T_j} u(X, T_j)$$
#### Định nghĩa 18: Chỉ mục tối đa của batch cũ trong TidList(Maximum Index of Old Batches in Tidlist)
Vỡi mỗi TWAE-Lists được khởi tạo từ cửa sổ trượt $W_n$, mỗi itemset X duy trì các thông tin liên quan tới nó thông qua một tidlist. Chỉ mục tối đa của các giao dịch từ các batch cũ được định nghĩa là $OldIndex(X, W_n)$ 

#### Định nghĩa 19: Cấu trúc TWAE-List
TWAE-List của một itemset X được định nghĩa là AEL(X). Trong hình 2, phần thông tin tiện ích ở mức độ cửa sổ bao gồm 6 trường chính: $U(X, W_n)$, $EAEUB(X,W_n)$, $Inv(X)$, $PI(X)$, $OldU(X,W_n)$, và $OldIndex(X,W_n)$. Các trường này tạo điều kiện thuận lợi để xóa giao dịch trong khi cửa sổ trượt

Thông tin tiện ích ở mức độ giao dịch được duy trì trong cấu trúc gọi là tidlist. Cấu trúc này bao gồm nhiều tuple $\langle T_j, U(X, T_j), RU(X, T_j), PU(X, T_j), minInv(X, T_j) \rangle$ được thiết kế để ghi lại tiện ích, tiện ích còn lại, tiện ích tiền tố, và mức độ đầu tư tối thiểu còn lại của itemset X trong từng giao dịch

#### 4.3.1 Quá trình khởi tạo TWAE-List  1-itemset
Thuật toán duy trì một cấu trúc danh sách AELs toàn cục, lưu trữ TWAE-List của từng item trong cửa sổ trượt hiện tại

B1: Sau khi batch đầu tiên tới, thuật toán quét các giao dịch trong batch, tính MAEUB cho từng 1-itemset
B2: Thêm nó vào TWAE-List một tuple có giá trị ($T_j$,$U(i_t,T_j),0,0,0$) 
B3:  Khi cửa sổ đã đầy batch, thuật toán cập nhật TWAE-Lists
* Chọn TWAE-Lists của item với tiềm năng hiệu suất trung bình cao
* Sắp xếp thêm thứu tự tăng dần giá trị MAEUB
* Duyệt TWAE-List theo thứ tự ngược lại, cập nhật giao dịch và mức độ đầu tư 
Quy trình diễn ra chi tiết như sau (Thuật toán 1 mô tả quá trình gán TWAE-Lists cho 1-itemset thỏa mãn ngưỡng hiệu quả trung bình tối thiểu trong cửa sổ trượt hiện tại):
* Thuật toán lọc AEL(X) từ TWAE-Lists toàn cục có $MAEUB(X,W_n) \gt minae$ và thêm chúng vào AELRecursion
* Mảng RU và INV được khởi tạo để lưu trữ giá trị tiện ích còn lại và mức độ đầu tư tối thiểu với độ dài mảng MaxTid + 1
* Thuật toán tính toán các định danh biên của lô hết hạn dựa trên các giá trị của winNumber và batchSize, tạo ra maxOldBatchTid và minOldBatchTid
* Tiếp theo, thuật toán duyệt qua từng TWAE-List trong AELRecursion theo thứ tự ngược và lặp lại qua từng tuple ex trong danh sách định danh giao dịch tidlist (Dòng 10-12). Nếu giao dịch thuộc về lô cũ (tức là ex.tid ≤ maxOldBatchTid), nó tiếp tục kiểm tra xem giao dịch có vượt quá phạm vi cửa sổ hiện tại hay không (tức là ex.tid ≤ minOldBatchTid). Nếu vượt quá phạm vi cửa sổ, tuple sẽ được loại bỏ khỏi tidlist và giá trị độ hữu dụng U(X, Wn) của AEL(X) được cập nhật (Dòng 13-17). Ngược lại, tuple được đánh dấu là giao dịch lô cũ, vị trí chỉ mục index của nó được ghi lại, và giá trị độ hữu dụng OldU được tích lũy
* Sau đó, đối với mỗi tuple, độ hữu dụng còn lại RU được tính toán (Dòng 22). Thuật toán sau đó kiểm tra xem mảng đầu tư còn lại tối thiểu INV đã được khởi tạo chưa. Nếu có, giá trị EAEUB tương ứng cho ex được thêm vào AEL(X).EAEUB, và đầu tư còn lại tối thiểu được cập nhật tiếp theo (Dòng 23-32). Cuối cùng, mảng RU được cập nhật.
![[Pasted image 20251126201053.png]]
![[Pasted image 20251126201107.png]]

Ví dụ, giả sử ngưỡng hiệu suất trung bình tối thiểu minae = 0.25. Theo chiến thuật cắt tỉa MAEUB, khởi tạo tất cả TWAE-Lists trong $W_1$ thỏa $MAEUB(X,W_1) \ge minae$ và nhận d ≺ a ≺ e ≺ f ≺ b ≺ c  theo thứ tự tăng dần MAEUB. Hình 3 cho thấy TWAE-List toàn cục được khởi tạo trong giai đoạn khởi tạo dựa trên giao dịch trong $W_1$. Do đó, TWAE-List toàn cục được gán dựa theo quá trình trong thuật toán 1. Đầu tiên, TWAE-Lists ánh xạ tới item thõa ngưỡng hiệu suất trung bình tối thiểu được lọc. Vì $MAEUB(a,W_1) = 0.183 < minae)$, $MAEUB(d,W_1) = 0.136 < minae$
$MAEUB(e,W_1) = 0.233 < minae$, quá trình xẩy dựng TWAE-Lists cho {a,d,e} là không cần thiết. TWAE-Lists sau quá trình gán có kết quả như hình 4

#### 4.3.2 Quá trình khởi tạo TWAE-List cho m-itemset