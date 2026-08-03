# Reflection — Nguyễn Minh Hiếu (2A202601154)

## Vai trò

Data — thu thập dữ liệu, thử nghiệm sản phẩm và hỗ trợ validation với người dùng.

## Phần tôi thực hiện

- Thu thập và tổng hợp dữ liệu khảo sát để kiểm tra pain của học viên khi tự học; kết quả được dùng trong spec là 15/22 người ngoài nhóm (68,2%) xác nhận khó tìm câu trả lời tức thì.
- Thử nghiệm sản phẩm qua các tình huống chat thực tế, ghi nhận kết quả pass/fail và phối hợp tổng hợp feedback người dùng từ Telegram, Discord và dashboard.
- Cập nhật phần evidence, kết quả khảo sát và thông tin sản phẩm vào tài liệu nhóm để quyết định chọn bài toán dựa trên số liệu thay vì chỉ dựa vào cảm nhận.

Bằng chứng liên quan gồm [AI Spec](../spec.md) §1–§2, [file khảo sát](../eval/Survey_GG_form.xlsx), [golden set](../eval/test_cases.md) và [feedback log](../validation/feedback_issue.md).

## AI hỗ trợ thế nào

Tôi dùng AI để gợi ý cách diễn đạt câu hỏi khảo sát, nhóm các phản hồi theo chủ đề và tạo khung ghi nhận kết quả test. Sau đó tôi kiểm tra thủ công số người trả lời, tỷ lệ, câu quote và trạng thái từng case trước khi đưa vào artifact. Việc này quan trọng vì AI có thể tóm tắt rất trôi chảy nhưng vẫn bỏ mất ngoại lệ hoặc làm sai con số.

## Bài học từ case fail của nhóm

Phiên test Discord đầu tiên đạt 8/10 case, nhưng hai case fail gồm một lần bịa nội dung và một quiz không dựa trên tài liệu/không có trích nguồn. Con số 80% nhìn riêng có vẻ chạm ngưỡng, nhưng nhóm vẫn **không đạt** quality bar vì vi phạm điều kiện cứng “không bịa trích nguồn dù một lần”. Tôi học được rằng validation không thể chỉ báo cáo tỷ lệ pass: phải lưu đủ case fail, điều kiện pass/fail và nguyên nhân. Lần sau tôi sẽ ưu tiên chạy các case rủi ro cao trước, rồi mới dùng tỷ lệ tổng để kết luận chất lượng.
