**Định nghĩa:** dUB table là bảng lưu trữ giá trị cận trên suy giảm của các mục trong mô hình DMAUP. Giá trị dUB của một mục được tính bằng cách nhân cận trên trung bình (AUUB - Average Utility Upper Bound) với hệ số suy giảm (decaying factor).​

**Công thức:** dub(P)=∑T∈DBmu(T)×f(Tlast−T)dub(P)=∑T∈DBmu(T)×f(Tlast−T), trong đó ff là hệ số suy giảm, TlastTlast là giao dịch mới nhất, và mu(T)mu(T) là tiện ích tối đa của giao dịch.​

**Tác dụng:** dUB table được sử dụng để sắp xếp các dAList theo thứ tự tăng dần của giá trị dUB, giúp giảm không gian tìm kiếm và cắt tỉa các mẫu không triển vọng trong quá trình khai phá mẫu tiện ích trung bình suy giảm.​