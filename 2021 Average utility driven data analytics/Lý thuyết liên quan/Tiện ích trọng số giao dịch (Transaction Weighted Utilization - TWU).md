Đây là một khái niệm quan trọng trong khai phá mẫu tiện ích cao được đề xuất để đảm bảo tính chất phản đơn điệu (antimonotone property). TWU được định nghĩa là tổng tiện ích của một giao dịch chứa một mẫu cụ thể trong toàn bộ cơ sở dữ liệu.​

## Công thức

TWU của một mẫu XX được tính như sau:​

TWU(X)=∑X⊆T∧T∈DBTU(T)TWU(X)=∑X⊆T∧T∈DBTU(T)

Trong đó TU(T)TU(T) là tiện ích giao dịch (transaction utility) của giao dịch TT, và DBDB là cơ sở dữ liệu.

## Vai trò và ưu điểm

**Đảm bảo tính phản đơn điệu:** TWU được thiết kế để thỏa mãn tính chất phản đơn điệu trong khai phá mẫu tiện ích cao, nghĩa là nếu TWU của một mẫu nhỏ hơn ngưỡng tiện ích tối thiểu, thì tất cả các mẫu mở rộng của nó cũng không thể là mẫu tiện ích cao.​

**Giảm không gian tìm kiếm:** Nhờ tính chất phản đơn điệu của TWU, các mẫu không triển vọng có thể được loại bỏ sớm trong quá trình khai phá, giúp giảm đáng kể không gian tìm kiếm và cải thiện hiệu suất.​

**Ứng dụng trong thuật toán:** TWU được sử dụng rộng rãi trong các thuật toán khai phá tiện ích cao như Two-Phase, UP-Growth, và nhiều thuật toán hiện đại khác để xác định các mẫu ứng viên có tiềm năng cao trước khi tính toán tiện ích thực tế của chúng.​