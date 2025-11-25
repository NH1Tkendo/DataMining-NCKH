Phương pháp này ra đời nhằm giải quyết vấn đề của các cách tiếp cận trước đó mà không chú ý tới cả tần suất và lợi nhuận của từng mẫu. HUPM không thỏa mãn [[Tính chất phản đơn điệu (Antimonotone)]]. Do đó, [[Tiện ích trọng số giao dịch (Transaction Weighted Utilization - TWU)]] được đề xuất để khắc phục nhược điểm này. Nhưng mà cách này lại quét database nhiều lần và tạo nhiều mẫu ứng cử viên. [[Tăng trưởng mẫu tiện ích (Utility Pattern Growth)]] có hiệu suất cao hơn các thuật toán Apriori-like, đi kèm theo là các nhược điểm như tạo ra nhiều ứng cử viên hoặc sử dụng tốn bộ nhớ. Để giải quyết những vấn đề này. Để giải quyết những vấn đề còn tồn đọng, [[HUI-Miner]] áp dụng một cấu trúc thuật giải giúp không tạo ra ứng cử viên khi khai thác dữ liệu. Sau đó là sự ra đời của các thuật toán tiên tiến hơn như HUP-Miner, FHM, FHM+ có các chiến thuật [[Cắt tỉa (Pruning)]] hiệu quả hơn. Cuối cùng là [[IMHUP (Improved Mining of High Utility Patterns)]] thực thi khai thác các mẫu hiệu dụng cao với danh sách có chỉ mục.

Để giải quyết với vấn đề xử lý dữ liệu thời gian thực, nhiều kỹ thuật khai thác loại dữ liệu này đã được đưa ra.
 * [[IUM (Incremental Utility Mining)]] và [[FIUM (Fast Incremental Utility Mining)]] quét cơ sở dữ liệu vài lần để tạo ra một lượng lớn các ứng cử viên 
 * [[IHUP]] và [[HUPID (High Utility Pattern mining in Incremental Databases)]]
 
 Những thuật toán ở trên đều cần thêm thời gian xử lý và bộ nhớ khi chúng tạo các ứng cử viên.
 
 * [[LIHUP (List-based Incremental High Utility Pattern mining)]]
 * [[IIHUM (Indexed Incremental High Utility Mining)]]
