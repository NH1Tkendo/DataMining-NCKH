Đây là một thuật toán hiệu quả được đề xuất bởi Liu & Qu (CIKM 2012) để khai phá các tập mục tiện ích cao (high utility itemsets) trong cơ sở dữ liệu giao dịch mà không cần tạo ra các tập ứng viên (candidate generation). HUI-Miner được thiết kế để khắc phục nhược điểm của các thuật toán hai pha (two-phase algorithms) truyền thống bằng cách trực tiếp tính toán tiện ích của các tập mục trong một giai đoạn duy nhất.[](https://philippe-fournier-viger.com/spmf/HUI-Miner.php)​

## Cấu trúc dữ liệu chính

**Utility-List (Danh sách tiện ích):** HUI-Miner sử dụng một cấu trúc mới gọi là utility-list để lưu trữ cả thông tin tiện ích về một tập mục và thông tin heuristic để cắt tỉa không gian tìm kiếm. Mỗi utility-list chứa thông tin về tiện ích của một tập mục trong từng giao dịch, bao gồm TID (transaction ID), iutil (item utility), và rutil (remaining utility).[](https://dl.acm.org/doi/10.1145/2396761.2396773)​

## Cách hoạt động

**Quét cơ sở dữ liệu một lần:** HUI-Miner chỉ cần quét cơ sở dữ liệu một lần để xây dựng utility-list cho mỗi mục đơn.[](https://philippe-fournier-viger.com/spmf/ULB_MINER_Utility.pdf)​

**Xây dựng utility-list đệ quy:** Sau đó, thuật toán xây dựng đệ quy các utility-list cho các tập mục lớn hơn bằng cách nối (join) các utility-list của các tập mục con của chúng mà không cần quét lại cơ sở dữ liệu.[](https://philippe-fournier-viger.com/spmf/HUI-Miner.php)​

**Tính toán trực tiếp:** HUI-Miner có thể tính toán trực tiếp tiện ích của các tập mục từ utility-list và sử dụng cận trên (upper-bounds) để giảm không gian tìm kiếm mà không cần duy trì một tập lớn các ứng viên trong bộ nhớ.[](https://dl.acm.org/doi/10.1145/2396761.2396773)​

## Ưu điểm

**Không tạo ứng viên:** Khác với các thuật toán hai pha, HUI-Miner không cần tạo ra các tập ứng viên, giúp giảm đáng kể việc sử dụng bộ nhớ.[](https://philippe-fournier-viger.com/spmf/ULB_MINER_Utility.pdf)​

**Tránh quét lặp lại:** Thuật toán tránh được việc phải quét cơ sở dữ liệu nhiều lần để tính toán tiện ích của các tập mục.[](https://philippe-fournier-viger.com/spmf/HUI-Miner.php)​

**Hiệu suất cao:** HUI-Miner được chứng minh là nhanh hơn nhiều so với các thuật toán trước đó như UP-Growth (nhanh hơn đến 100 lần) và Two-Phase (nhanh hơn đến 1000 lần). Tuy nhiên, các thuật toán mới hơn như FHM (2014) và EFIM (2015) đã vượt qua HUI-Miner về hiệu suất.