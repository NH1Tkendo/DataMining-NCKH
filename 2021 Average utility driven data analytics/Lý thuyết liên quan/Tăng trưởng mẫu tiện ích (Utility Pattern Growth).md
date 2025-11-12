Đây là một thuật toán hiệu quả được đề xuất bởi Tseng và cộng sự (KDD 2010) để khai phá các tập mục tiện ích cao (high utility itemsets) trong cơ sở dữ liệu giao dịch. UP-Growth được thiết kế để khắc phục các hạn chế của các phương pháp trước đó bằng cách giảm số lượng ứng viên được tạo ra và cải thiện hiệu suất khai phá.[philippe-fournier-viger+2](https://www.philippe-fournier-viger.com/spmf/UPGrowthPlus.php)​

## Cấu trúc dữ liệu chính

**UP-Tree (Utility Pattern Tree):** UP-Growth sử dụng cấu trúc cây UP-Tree toàn cục để duy trì thông tin về các giao dịch và tập mục một cách hiệu quả. Cây này chỉ cần quét cơ sở dữ liệu hai lần, giúp tránh việc quét lặp lại nhiều lần.[arxiv+1](https://arxiv.org/pdf/1212.0317.pdf)​

## Bốn chiến lược cắt tỉa

UP-Growth phát triển bốn chiến lược hiệu quả để cắt tỉa ứng viên trong giai đoạn I:[slideserve](https://www.slideserve.com/tomasab/up-growth-an-efficient-algorithm-for-high-utility-itemset-mining-powerpoint-ppt-presentation)​

- **DGU (Discarding Global Unpromising items):** Loại bỏ các mục không triển vọng toàn cục và tiện ích của chúng khỏi tiện ích giao dịch[slideserve+1](https://www.slideserve.com/tomasab/up-growth-an-efficient-algorithm-for-high-utility-itemset-mining-powerpoint-ppt-presentation)​
    
- **DGN (Discarding Global Node utilities):** Giảm tiện ích của các nút gần gốc cây UP-Tree toàn cục trong quá trình xây dựng[arxiv+1](https://arxiv.org/pdf/1212.0317.pdf)​
    
- **DLU (Discarding Local Unpromising items):** Loại bỏ tiện ích của các mục không triển vọng cục bộ khỏi tiện ích đường đi[slideserve+1](https://www.slideserve.com/tomasab/up-growth-an-efficient-algorithm-for-high-utility-itemset-mining-powerpoint-ppt-presentation)​
    
- **DLN (Discarding Local Node utilities):** Loại bỏ tiện ích của các nút con cháu trong quá trình xây dựng cây UP-Tree cục bộ[arxiv+1](https://arxiv.org/pdf/1212.0317.pdf)​
    

## Ưu điểm

**Giảm số lượng ứng viên:** UP-Growth giảm đáng kể số lượng tập mục ứng viên được tạo ra trong giai đoạn I so với các phương pháp truyền thống.[acm+1](https://dl.acm.org/doi/10.1145/1835804.1835839)​

**Hiệu suất cao:** Kết quả thực nghiệm cho thấy UP-Growth vượt trội hơn đáng kể so với các thuật toán khác, đặc biệt khi cơ sở dữ liệu chứa nhiều giao dịch dài hoặc khi ngưỡng tiện ích tối thiểu thấp.[semanticscholar+2](https://www.semanticscholar.org/paper/UP-Growth:-an-efficient-algorithm-for-high-utility-Tseng-Wu/a579bb390da6d2a164144a57a7b731cf0ab20d8b)​

**Tránh quét lặp lại:** Bằng cách sử dụng UP-Tree, thuật toán tránh được việc phải quét cơ sở dữ liệu gốc nhiều lần, cải thiện đáng kể tốc độ xử lý.[arxiv+1](https://arxiv.org/abs/1212.0317)​