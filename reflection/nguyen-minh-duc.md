# Reflection — Nguyễn Minh Đức (2A202601946)

## Vai trò
Data (xử lý data, góp ý kiến trúc Agent) — chịu trách nhiệm phần dữ liệu đầu vào cho RAG pipeline của Vlearn Agent và tham gia thảo luận thiết kế kiến trúc agent cùng cả nhóm.

## Phần mình làm
- **Cào dữ liệu:** thu thập nguyên liệu thô cho vault (slide, transcript bài giảng, tài liệu tham khảo) từ data pack của khoá để có đủ nội dung nạp vào hệ thống.
- **Xử lý dữ liệu:** làm sạch, cấu trúc hoá raw text thành markdown có heading/bullet — đúng format mà `ingest/structurer.py` và vault (kiểu Obsidian) cần, để agent đọc và trích dẫn được chính xác (tên bài, slide, trang).
- **Embedding thành knowledge base:** đưa dữ liệu đã xử lý qua bước embedding (Voyage AI) và nạp vào Chroma vector store, để agent trả lời bằng **semantic search trên KB đã index sẵn** thay vì phải quét/tìm trực tiếp trên log chat thật mỗi lần có câu hỏi — vừa nhanh hơn, vừa không phải phụ thuộc dữ liệu log nhạy cảm để suy luận câu trả lời.
- **Góp ý kiến trúc:** tham gia bàn với Hoàng (Lead) về việc giữ agent ở mức **augment** thay vì automate hoàn toàn (cost-of-error cao nếu bịa kiến thức chuyên môn), và về nguyên tắc bắt buộc trích nguồn cho mọi câu trả lời — xuất phát từ việc hiểu rõ dữ liệu nguồn có những khoảng trống/mâu thuẫn gì (VD: slide và thông báo lệch deadline — kịch bản lỗi lớp 4 trong spec §5).

## AI hỗ trợ thế nào
Dùng AI (trợ lý coding) để tăng tốc các bước lặp lại và tốn effort thủ công nếu làm tay:
- Viết/sửa script cào và làm sạch dữ liệu thô từ slide/transcript.
- Gợi ý cấu trúc markdown chuẩn (heading, bullet, code block) để đồng bộ với format `structurer.py` đang dùng trong pipeline.
- Kiểm tra nhanh kết quả embedding có match đúng nội dung khi thử semantic search thử trên vài câu hỏi mẫu, trước khi bàn giao KB cho phần build của Hoàng.
Vẫn tự kiểm tra lại thủ công từng bước — đặc biệt là bước cấu trúc hoá, vì AI có thể tự "làm gọn" nội dung khiến sai lệch so với tài liệu gốc, điều tối kỵ với một sản phẩm cam kết "không bịa".

## Bài học từ case fail của nhóm
Ở lượt kiểm thử đầu (30/07/2026, model `gpt-4o-mini`), agent **bịa nội dung** ở 1/10 case và **trả lời quiz không kèm trích nguồn** ở 1 case khác — dù dữ liệu đúng đã có sẵn trong KB. Bài học rút ra: **có KB đầy đủ và embedding đúng không tự động đảm bảo output đúng** — retrieval tốt là điều kiện cần, nhưng quality bar ("không bịa trích nguồn dù 1 lần") phải được test riêng ở tầng generation, không thể coi là "xong" chỉ vì bước xử lý/embedding dữ liệu đã chạy sạch. Lần sau mình sẽ chủ động đề xuất thêm case kiểm thử ngay từ khi bàn giao KB, thay vì chỉ dừng ở việc xác nhận dữ liệu đã nạp đúng.
