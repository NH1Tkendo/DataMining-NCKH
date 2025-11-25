Đây là một thuật toán hybrid (lai ghép) được thiết kế để giảm số lượng các thao tác nối (join operations) cần thiết trong các phương pháp dựa trên utility-list. IMHUP sử dụng cấu trúc dữ liệu indexed-list (danh sách được đánh chỉ mục) để cải tiến cấu trúc dữ liệu dựa trên danh sách hiện có và không tạo ra các mẫu ứng viên trong quá trình khai phá.[](https://2024.sci-hub.se/8296/0a6af31b3ba1bccb33bf8075e445cec2/sohrabi2020.pdf)​

## Đặc điểm chính

**Cấu trúc indexed-list:** IMHUP giới thiệu cấu trúc IU-List (Indexed Utility List) thay vì utility-list truyền thống, giúp giảm chi phí tính toán và bộ nhớ.[](https://2024.sci-hub.se/8296/0a6af31b3ba1bccb33bf8075e445cec2/sohrabi2020.pdf)​

**Phương pháp hybrid:** IMHUP kết hợp ưu điểm của cả phương pháp dựa trên cây (tree-based) và phương pháp dựa trên danh sách (list-based) để tối ưu hóa hiệu suất.[](https://2024.sci-hub.se/8296/0a6af31b3ba1bccb33bf8075e445cec2/sohrabi2020.pdf)​

## Các biến thể

IMHUP có nhiều phiên bản cải tiến:[](https://2024.sci-hub.se/8296/0a6af31b3ba1bccb33bf8075e445cec2/sohrabi2020.pdf)​

- **IMHUP-RUI:** Sử dụng kỹ thuật giảm cận trên tiện ích trong IU-Lists
    
- **IMHUP-CHI:** Kết hợp các mục tiện ích cao
    
- **IMHUP-RUI&CHI:** Kết hợp cả hai kỹ thuật trên
    

## Hiệu suất

**So sánh với FHM:** IMHUP nhanh hơn khoảng 2-12 lần so với thuật toán FHM (Fast High-Utility Miner).[](https://pdfs.semanticscholar.org/d245/37d52bb5eb233f58a23d02c1d20f1f6b1c25.pdf)​

**So sánh với EFIM:** Tuy nhiên, IMHUP không vượt trội hơn thuật toán EFIM (Efficient high-utility Itemset Mining), một trong những thuật toán hiệu quả nhất hiện nay.[](https://pdfs.semanticscholar.org/d245/37d52bb5eb233f58a23d02c1d20f1f6b1c25.pdf)​

**Ứng dụng:** IMHUP được sử dụng để khám phá các tập mục tiện ích cao trong cơ sở dữ liệu giao dịch, đặc biệt hữu ích trong phân tích giỏ hàng để tìm ra các nhóm sản phẩm tạo ra lợi nhuận cao nhất.[](https://www.sciencedirect.com/science/article/abs/pii/S0952197617303159)​
