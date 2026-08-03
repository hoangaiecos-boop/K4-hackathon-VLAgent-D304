# Reflection — Trần Thanh Huyền (2A202601578)

## Vai trò

Documentation — viết tài liệu báo cáo và tổng hợp evidence để các quyết định của nhóm có thể kiểm tra lại.

## Phần tôi thực hiện

- Chuẩn hoá phần trình bày của sản phẩm thành tài liệu: problem, tác động, thiết kế, rủi ro, kiểm thử và validation.
- Tổng hợp evidence từ khảo sát và feedback thành số liệu, quote và liên kết tới artifact nguồn để phần spec không chỉ dừng ở mô tả tính năng.
- Ghi nhận phản hồi người dùng cùng thay đổi nhóm thực hiện sau validation, đặc biệt phản hồi về khó khăn khi cài đặt bot.
- Rà sự nhất quán giữa README, spec, bộ test và feedback log để người đọc có thể lần từ kết luận về nguồn kiểm chứng.

Các tài liệu tôi đối chiếu là [AI Spec](../spec.md), [feedback log](../validation/feedback_issue.md) và [bộ test](../eval/test_cases.md).

## AI hỗ trợ thế nào

AI giúp tôi dựng khung tài liệu, chuẩn hoá câu chữ và rà các điểm thiếu liên kết giữa các phần. Tôi không dùng AI để tự tạo số liệu, quote hoặc kết quả kiểm thử: từng con số và phản hồi được kiểm tra lại với file nguồn trước khi ghi vào báo cáo. Với evidence, văn phong hay không thay thế được khả năng truy vết.

## Bài học từ case fail của nhóm

Trong validation, người dùng `@nguynthithuha05-del` phản hồi rằng phần cài đặt bot khó với người chưa có nền tảng kỹ thuật. Case này cho thấy một README có đủ hướng dẫn vẫn có thể thất bại nếu người mới không biết bắt đầu từ đâu. Nhóm đã bổ sung quy trình setup đơn giản hơn, nhưng bài học của tôi là tài liệu phải được đánh giá bằng task thật của người dùng, không phải bằng cảm giác “đã viết đủ”. Lần sau tôi sẽ thêm checklist theo hệ điều hành và test onboarding với người chưa từng chạy dự án trước khi chốt tài liệu.
