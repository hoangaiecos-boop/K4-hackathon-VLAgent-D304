# Reflection — Nguyễn Minh Đức (2A202601946)

## Vai trò
Data (xử lý data, góp ý kiến trúc Agent) — chịu trách nhiệm phần dữ liệu đầu vào cho RAG pipeline của Vlearn Agent và tham gia thảo luận thiết kế kiến trúc agent cùng cả nhóm.

## Phần mình làm
- **Cào dữ liệu:** thu thập nguyên liệu thô cho vault (slide, transcript bài giảng, tài liệu tham khảo) từ data pack của khoá — khác với phần dữ liệu khảo sát/survey mà Hiếu phụ trách, đây là dữ liệu nội dung học thuật để nạp kiến thức cho agent.
- **Xử lý dữ liệu:** làm sạch, cấu trúc hoá raw text thành markdown có heading/bullet, đưa qua pipeline ingest sẵn có của hệ thống để agent đọc và trích dẫn được chính xác (tên bài, slide, trang) — không sửa code pipeline, chỉ chuẩn bị và đẩy dữ liệu qua đúng format nó yêu cầu.
- **Embedding thành knowledge base:** chạy dữ liệu đã xử lý qua bước embedding (Voyage AI) để nạp vào Chroma vector store, để agent trả lời bằng **semantic search trên KB đã index sẵn** thay vì phải quét/tìm trực tiếp trên log chat thật mỗi lần có câu hỏi — vừa nhanh hơn, vừa không phải phụ thuộc dữ liệu log nhạy cảm để suy luận câu trả lời.
- **Đóng góp cho thảo luận kiến trúc:** trong lúc xử lý dữ liệu, mình phát hiện một số khoảng trống/mâu thuẫn giữa các nguồn (VD: slide và thông báo lệch deadline — kịch bản lỗi lớp 4 trong spec §5). Mình đưa các quan sát này cho Hoàng (Lead) làm căn cứ thực tế cho quyết định giữ agent ở mức **augment** và bắt buộc trích nguồn mọi câu trả lời — quyết định kiến trúc cuối cùng do Hoàng chốt và triển khai.
- **Phát hiện dữ liệu mâu thuẫn thật (03/08/2026):** khi rà lại vault pack, phát hiện 4 bản trùng tên bài `day03-tu-chatbot-den-agentic-agent-react` có mục lục khác nhau (10/9/8/8 mục) — bằng chứng cụ thể cho rủi ro trích nguồn không nhất quán nếu bật song song nhiều nguồn cho cùng một bài. Ghi lại chi tiết và đề xuất xử lý trong [`eval/data-quality-notes.md`](../eval/data-quality-notes.md), không tự xoá/chọn bản canonical vì thiếu slide gốc để đối chiếu.

## AI hỗ trợ thế nào
Dùng AI (trợ lý coding) để tăng tốc các bước lặp lại và tốn effort thủ công nếu làm tay:
- Viết/sửa script cào và làm sạch dữ liệu thô từ slide/transcript.
- Gợi ý cấu trúc markdown chuẩn (heading, bullet, code block) để khớp với format mà pipeline ingest của hệ thống đang yêu cầu.
- Kiểm tra nhanh kết quả embedding có match đúng nội dung khi thử semantic search thử trên vài câu hỏi mẫu, trước khi bàn giao KB cho phần build của Hoàng.
Vẫn tự kiểm tra lại thủ công từng bước — đặc biệt là bước cấu trúc hoá, vì AI có thể tự "làm gọn" nội dung khiến sai lệch so với tài liệu gốc, điều tối kỵ với một sản phẩm cam kết "không bịa".

## Bài học từ case fail của nhóm
Ở lượt kiểm thử đầu (30/07/2026, model `gpt-4o-mini`), agent **bịa nội dung** ở 1/10 case và **trả lời quiz không kèm trích nguồn** ở 1 case khác — dù dữ liệu đúng đã có sẵn trong KB. Bài học rút ra: **có KB đầy đủ và embedding đúng không tự động đảm bảo output đúng** — retrieval tốt là điều kiện cần, nhưng quality bar ("không bịa trích nguồn dù 1 lần") phải được test riêng ở tầng generation, không thể coi là "xong" chỉ vì bước xử lý/embedding dữ liệu đã chạy sạch. Lần sau mình sẽ chủ động đề xuất thêm case kiểm thử ngay từ khi bàn giao KB, thay vì chỉ dừng ở việc xác nhận dữ liệu đã nạp đúng.
