# Ghi chú chất lượng dữ liệu — vault `packs/vlearn-pack`

> Người ghi: Nguyễn Minh Đức (xử lý data). Mục đích: log các phát hiện về dữ liệu nguồn mâu thuẫn/trùng lặp phát hiện khi xử lý & nạp vault — làm bằng chứng cụ thể cho kịch bản lỗi lớp 4 ("tài liệu mâu thuẫn") trong [spec.md §5](../spec.md).

## Phát hiện: 4 bản trùng tên bài `day03-tu-chatbot-den-agentic-agent-react` có nội dung khác nhau

Thư mục `learning-agent/vault/courses/packs/vlearn-pack/vlearn-pack/slides/` chứa 4 file cho cùng một bài (Ngày 3 — Từ Chatbot Đến Agentic Agent), khác nhau cả về độ dài lẫn nội dung mục lục ("Slide 2/3 — Nội Dung Bài Học"):

| File | Số dòng | Mục lục liệt kê |
|---|---|---|
| `day03-tu-chatbot-den-agentic-agent-react-v7.md` | 926 | 10 mục — có thêm "ReAct vs Function Calling", "Cost & Security", "Lab 3 + Rubric" |
| `day03-tu-chatbot-den-agentic-agent-react_hieu_e403.md` | 265 | 9 mục — có "Eval-Telemetry" (không có ở bản khác) |
| `day03-tu-chatbot-den-agentic-agent-react_manh.md` | 395 | 8 mục |
| `day03-tu-chatbot-den-agentic-agent-react_manh_v2.md` | 256 | 8 mục, nhưng đánh số **Slide 2** thay vì Slide 3 cho cùng mục "Nội Dung Bài Học" |

Chỉ riêng `AI20K/day03-tu-chatbot-den-agentic-agent-react-v7.md` được đưa vào course chính `AI20K`; 4 bản trên nằm trong Knowledge Pack `packs/vlearn-pack` (cài qua `updater/packs.py`) — nếu pack này được bật/index cùng lúc với `AI20K`, agent có thể trích 2 nguồn khác nhau cho cùng một câu hỏi về nội dung Ngày 3, dẫn đến trích nguồn không nhất quán (đúng loại lỗi mô tả ở spec §5, lớp 4, ví dụ 7-8).

## Vì sao chưa tự sửa
Không có slide gốc (PDF/bản giảng viên công bố) để xác định bản nào là canonical — 3 bản `_hieu_e403`, `_manh`, `_manh_v2` có tên gắn với người khác nhau, nhiều khả năng là ghi chú cá nhân của học viên khác nhau upload qua Knowledge Pack, không phải bản chính thức. Tự chọn/xoá bừa rủi ro làm mất nội dung đúng.

## Đề xuất
1. Trước khi bật pack `vlearn-pack` cùng course `AI20K` trong production, xác nhận với người tạo `_manh`/`_hieu_e403` xem đây có phải bản chính thức không.
2. Nếu không xác nhận được, chỉ giữ 1 bản (khuyến nghị `-v7` vì đã được đưa vào `AI20K` — course chính) làm nguồn duy nhất cho câu hỏi về Ngày 3, tránh index song song nhiều bản khác nhau của cùng một bài.
3. Bổ sung ≥1 case vào golden set (`eval/test_cases.md`) kiểm tra tình huống 2 nguồn nói khác nhau về cùng nội dung Ngày 3, để lộ hành vi agent khi gặp mâu thuẫn nguồn thật (hiện golden set chỉ có case mâu thuẫn giả định — spec §5 ví dụ 7 dùng deadline, chưa có case dựa trên mâu thuẫn dữ liệu thật này).
