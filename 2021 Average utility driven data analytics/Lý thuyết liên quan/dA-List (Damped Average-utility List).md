**Định nghĩa:** dA-List (hay dAList) là cấu trúc dữ liệu danh sách được thiết kế đặc biệt để khai phá mẫu tiện ích trung bình cao từ mô hình cửa sổ suy giảm. Mỗi dA-List tương ứng với một mục hoặc mẫu.​

**Cấu trúc:** Một dA-List bao gồm:​

- **Pattern (Mẫu):** Tên mục hoặc mẫu mà dAList đại diện
    
- **MRN (Maximum number of Remaining items):** Số lượng mục tối đa còn lại sau mẫu này
    
- **Các Tuple (bộ dữ liệu):** Mỗi tuple chứa:
    
    - TID (Transaction ID): Định danh giao dịch
        
    - Util: Tiện ích của mẫu trong giao dịch đó
        
    - MRU (Maximum Remaining Utility): Tiện ích tối đa của các mục còn lại sau mẫu này trong giao dịch
        

**Ưu điểm:** dA-List giúp loại bỏ dữ liệu không cần thiết, chỉ lưu trữ thông tin thiết yếu cần thiết để khai phá mẫu tiện ích trung bình cao. Nó cũng không tạo ra các mẫu ứng viên trong quá trình khai phá, giúp tiết kiệm bộ nhớ và thời gian xử lý so với các phương pháp truyền thống.​

**Quá trình xây dựng:** dA-List được xây dựng bằng cách quét từng giao dịch trong cơ sở dữ liệu và tính toán MRU, LEN cho từng mục. Khi có dữ liệu mới được chèn vào, dA-List được tái cấu trúc để phản ánh thông tin mới nhất từ cơ sở dữ liệu động.​

Những cấu trúc dữ liệu này (MU, dUB, dA-List) làm việc cùng nhau trong thuật toán DMAUP để cải thiện hiệu suất khai phá mẫu tiện ích trung bình cao từ các luồng dữ liệu động sử dụng mô hình cửa sổ suy giảm.​