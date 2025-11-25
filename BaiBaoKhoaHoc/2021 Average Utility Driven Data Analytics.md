
# **Phân tích dữ liệu hướng tiện ích trung bình trên cửa sổ suy giảm cho hệ thống thông minh với các luồng dữ liệu**

## Abstract (Tóm tắt)

* Trong các khu công nghiệp, hầu hết các cơ sở dữ liệu đều là [[Cơ sở dữ liệu động]] -> kích thước của csdl lớn dần theo thời gian
* Khai thác dữ liệu cho loại csdl này cần cách tiếp cận khác vì lợi nhuận hoặc độ chính xác của dữ liệu được chèn trước đó có thể giảm.
* Dữ liệu mới có giá trị cao hơn dữ liệu cũ
* Bài báo này đề xuất thuật toán phân tích dữ liệu hướng tiện ích trung bình trên cửa sổ trượt cho hệ thống thông minh (damped window based average utility driven data analytics for intelligent systems)
* Phương pháp khai thác đảm bảo cấu trúc dữ liệu thông thường, cung cấp nhiều chiến thuật [[Cắt tỉa (Pruning)]] và không tạo ứng cử viên.
* Thuật toán này tối ưu hơn về thời gian và bộ nhớ sử dụng so với các thuật toán khác 

## 1. Introduction (Giới thiệu)

* [[Khai thác dữ liệu (data mining)]]
* Đề cập tới các cách khai thác dữ liệu truyền thống
* Phương pháp khai thác dữ liệu động phải khác với dữ liệu tĩnh
* [[Mô hình cửa sổ trượt]] -> Không xử lý được dữ liệu thời gian thực
* [[Mô hình cửa sổ suy giảm (Damped window model)]] -> Được đề xuất để giải quyết vấn đề trên
* Bài báo này đề xuất thuật toán [[Damped Mining for Average Utility Pattern (DMAUP)]]
* Cách tiếp cận này từ từ giảm tiện ích trung bình của các giao dịch cũ dựa trên thời giai tới của chúng thay vì xóa chúng

Các đóng góp của bài báo này:
1. [[Damped Mining for Average Utility Pattern (DMAUP)]]
2. Các cấu trúc dữ liệu [[Maximum Utility Table (MU)]], [[Damped Upper-Bound Table (dUB)]], [[dA-List (Damped Average-utility List)]]
3. So sánh hiệu suất của thuật toán này với các thuật toán khác

## 2. Related work (công việc liên quan)

Phần này giới thiệu các phương pháp khai thác dữ liệu có liên quan tới bài báo này
* [[Khai thác mẫu hiệu suất cao ( High utility pattern mining)]]
* [[Khai thác mẫu tiện ích trung bình cao (High average utility pattern mining)]]
* [[Mô hình cửa sổ suy giảm (Damped window model)]]
## 3. Phân tích dữ liệu hướng tiện ích trung bình trên cửa sổ suy giảm

![[MiningApproach.png]]

Quy trình xây dựng
Bước 1: DMAUP quét cơ sở dữ liệu 
Bước 2: dA-List được tạo
Bước 3: Khởi tạo bảng MU (dùng để lưu tiện ích tối đa của từng giao dịch)
Bước 4: Khởi tạo bảng dUB (Lưu giá trị dUB của từng item) và làm mới mỗi lần được gọi. Phản ánh thời gian tới của tài liệu mới nhất thông qua decaying factor

Khi một người dùng gửi yêu cầu tới thì quy trình xây dựng sẽ được kích hoạt

## 3.1 Sơ lược

![[Bảng-Transaction.png]]

![[Bảng lợi nhuận.png]]

Các công thức tính toán:

**Định nghĩa 1:**
![[ItemUtility.png]]

**Định nghĩa 2:**
![[TransactionUtility.png]]

Ví dụ: tu(T1) = 8 + 12 + 5 = 25

**Định nghĩa 3:**
![[AverageUtility.png]]
l(P) -> Độ dài của mẫu P

Ví dụ:  au(AB) = (8 + 12)/2 + (8+12)/2 = 20

**Định nghĩa 4:**
![[MinimumAverageUtility.png]]
Nếu au(P) >= minAU thì P là mẫu tiện ích trung bình cao

**Định nghĩa 5:**
![[MaximumUtility.png]]

Ví dụ: mu(T1) = 12

**Định nghĩa 6:** Trung bình tiện ích cận trên (AUUB)
![[AverageUtilityUpperBound.png]]

Ví dụ: ub(A) = mu(T1) + mu(T3) + mu(T4) = 12 + 12 + 12 = 36

**Định nghĩa 7:** Tính chất phản đơn điệu trong khai thác mẫu tiện ích trung bình cao
Nếu ub(P) < minAU -> P và các siêu tập hợp của nó không thể mở rộng thành mẫu tiện ích trung bình cao

### Các định nghĩa cho mô hình cửa sổ suy giảm

**Định nghĩa 8:** Hệ số suy giảm đại diện cho mức độ quan trọng của một mẫu giảm dần theo thời gian. Có giá trị giữa 0 và 1. Nó lấy lũy thừa của hiệu số giữa thời điểm đến của giao dịch mới nhất và thời điểm của giao dịch mà mẫu PP xuất hiện

![[DecayingFactor.png]]

**Định nghĩa 9:** Hệ số trung bình tiện ích suy giảm (dAU) là kết quả của phép nhân số tiện ích trung bình của một mẫu và hệ số suy giảm của nó. dAU dùng để xác định mẫu tiện ích trung bình cao gần nhất.
![[DampedAverageUtility.png]]

Ví dụ: Xét mẫu A và hệ số suy giảm = 0.5 
=> dAU(A) = 15 

**Định nghĩa 10:**  Cận trên suy giảm (Damped upper-bound) được tính bằng cách lấy AUUB nhân cho hệ số suy giảm. 
![[Damped Upper-bound.png]]

Ví dụ: dub(A) = 19.5

**Định nghĩa 11:** Mẫu tiện ích trung bình cao gần nhất và tính chất phản đơn điệu trong khai thác mẫu tiện ích trung bình cao với mô hình cửa sổ suy giảm. 

Nếu trung bình tiện ích suy giảm của một mẫu ích hơn minAU, mẫu này không là mẫu trung bình tiện ích cao gần nhất. Ngược lại, nó là mẫu trung bình tiện ích cao gần nhất. dUB được sử dụng để cắt tỉa các mẫu không đủ điều kiện để trở thành mẫu trung bình tiện ích cao gần nhất trong tương lai. 

## 3.2 Khởi tạo dA-Lists từ cơ sở dữ liệu gốc

Các ý chính:
* dA-Lists được dùng để khai thác các mẫu trung bình tiện ích cao mà không tạo ra ứng cử viên.
* dA-Lists ánh xạ dữ liệu của chính mẫu nó chứa trong cơ sở dữ liệu
	* 1 mục trong dA-Lists chứa giá trị MRN và vài tuples
	* Mỗi tuple chứa id định danh, tiện ích, và MRU của mẫu đó
	* dA-List được lọc theo giá trị tăng dần của dUB

**Định nghĩa 12:** Tiện ích tối đa của các items còn lại (Maximum item utility of remaining items) đại diện cho giá trị tiện ích lớn nhất của các mẫu sau mẫu P, được kí hiệu là mru(P,T)
![[MaximumRemainingUtility.png]]

**Định nghĩa 13:**  Maximum number of the remaining items


Quá trình thực hiện DMAUP
Bước 1:  Bắt đầu từ dA-List đầu tiên. Xét dAL(P) -> Tính dau(P) nếu < minAU không là mẫu tiện ích trung bình cao gần nhất. Ngược lại thì là mẫu tiện ích trung bình cao gần nhất