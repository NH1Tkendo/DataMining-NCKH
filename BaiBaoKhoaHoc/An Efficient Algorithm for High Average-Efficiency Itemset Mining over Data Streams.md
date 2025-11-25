
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


