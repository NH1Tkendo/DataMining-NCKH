
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
* [[Mô hình cửa sổ suy giảm]] -> Được đề xuất để giải quyết vấn đề trên
* Bài báo này đề xuất thuật toán [[Damped Mining for Average Utility Pattern (DMAUP)]]
* Cách tiếp cận này từ từ giảm tiện ích trung bình của các giao dịch cũ dựa trên thời giai tới của chúng thay vì xóa chúng

Các đóng góp của bài báo này:
1. [[Damped Mining for Average Utility Pattern (DMAUP)]]
2. Các cấu trúc dữ liệu [[Maximum Utility Table (MU)]], [[Damped Upper-Bound Table (dUB)]], [[dA-List (Damped Average-utility List)]]
3. So sánh hiệu suất của thuật toán này với các thuật toán khác

## 2. Related work (công việc liên quan)