# AI Support Log

## AI đã giúp tôi ở đâu?

AI hỗ trợ hệ thống hóa bài làm từ core job, core action đến nature, cadence, metric system, retention và product loop. AI giúp diễn đạt rõ hành vi “CSKH review và hoàn tất xác minh một case”, gắn với event `case_verification_completed`, đồng thời trình bày công thức metric, mapping event và acceptance criteria để dễ rà soát tính nhất quán.

## AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?

Điểm cần phản biện là cách xếp **Median Verification Time** vào “depth”: chỉ số này phản ánh thời gian xử lý, chưa trực tiếp đo mức độ review đầy đủ. Thời gian giảm cũng chưa chứng minh chất lượng tăng, vì có thể do review qua loa hoặc khác biệt độ khó của case. Ngoài ra, dùng số lần hỏi AI hay D1/D7 login retention làm thước đo chính sẽ không phù hợp với nature **workflow + event-response**, do nhu cầu sử dụng phụ thuộc vào case được giao.

## Tôi đã tự sửa hoặc quyết định lại điều gì?

Tôi giữ core action ở hành vi của CSKH và chọn cadence **per case**, tổng hợp theo ca/ngày làm việc. Tôi chọn **Quality-Verified Case Rate (QVCR)** làm North Star Metric, đọc thời gian xác minh cùng **Rework Rate** và quality threshold để tránh chỉ tối ưu tốc độ. Retention chỉ xét các ca có case đủ điều kiện; không có cơ hội xử lý thì không tính là churn. Tôi cũng yêu cầu completion event chỉ ghi khi case thực sự chuyển bước và không bị ghi trùng do reload hoặc retry.
