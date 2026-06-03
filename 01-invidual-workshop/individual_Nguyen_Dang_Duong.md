# App Teardown — V-App / V-AI

# 1. Four Paths Overview

| Path | Test prompt | AI response hiện tại | Evidence |  
|---|---|---|---|
| Happy | Tìm nhà thuốc gần nhất | 6 nhà thuốc để lựa chọn: Cửa hàng FPT Long Châu, Nhà thuốc Pharmacity, ... | [Happy evidence](screenshots/z7896504931428_7b8e818c20e5063e9006e4c48740984a.jpg) |  
| Low-confidence | Tôi muốn đăng kí mua xe điện vinfast | Shows options hỏi kĩ lại người dùng là Ô tô điện hay xe máy điện | [Low-confidence evidence](screenshots/z7896522669329_a675a454b5a2321f711ac45184b09911.jpg) |  
| Failure | Tôi ko muốn bạn đưa ra các gợi ý tiếp theo sau mỗi phản hồi nữa (gây rối thông tin), sau đó hỏi lại hướng dẫn mua xe VF9 | V-AI đã ghi nhận yêu cầu, nhưng khi được hỏi lại thì vẫn show các gợi ý tiếp theo  | [Failure evidence](screenshots/z7896528924286_2724eac941760e6eef1956df47e2033a.jpg) và [Failure evidence](screenshots/z7896531289192_c46bdb3ffabb49b9f9b86bc1c3239325.jpg) |  
| Correction | Phát hiện và prompt lại là "Bạn vẫn đưa ra các gợi ý ? Tôi đã bảo là ko được đưa ra các gợi ý tiếp theo", rồi hỏi lại cách mua vf9 | V-AI vẫn đưa ra gợi ý, correction không được thực hiện | [Correction evidence](screenshots/z7896545949236_a8807289200b29e4bdaa943a9fb6ea93.jpg) và [Correction evidence](screenshots/z7896545983265_7d257c73af0981558eb9bd3930e0ea6e.jpg) |

# 2. Finding (product decision)

Khi user yêu cầu V-AI không đưa ra các gợi ý tiếp theo sau mỗi phản hồi, V-AI có ghi nhận yêu cầu nhưng không thật sự thay đổi hành vi ở các lượt hỏi sau.

AI/product failure: V-AI vẫn tiếp tục hiển thị các gợi ý tiếp theo dù user đã nói rõ rằng các gợi ý đó gây rối thông tin và không muốn thấy nữa.

Impact: User mất cảm giác kiểm soát cuộc hội thoại, phải nhắc lại cùng một yêu cầu nhiều lần, và trải nghiệm hỏi đáp trở nên kém tin cậy vì AI xác nhận đã hiểu nhưng không làm đúng.

Layer lỗi: UX Recovery + Memory/Instruction Following.

Product decision: V-AI cần có cơ chế ghi nhớ preference trong session hiện tại. Khi user yêu cầu tắt hoặc giảm một kiểu phản hồi, ví dụ không hiển thị suggestion chips/gợi ý tiếp theo, hệ thống phải áp dụng ngay cho các lượt sau trong cùng cuộc hội thoại.

Requirement đề xuất: Nếu user nói các câu như "đừng đưa ra gợi ý tiếp theo", "không cần gợi ý nữa", hoặc "các gợi ý này gây rối", V-AI phải:

- Xác nhận đã thay đổi cách phản hồi.
- Không hiển thị suggestion chips trong các câu trả lời tiếp theo của session hiện tại.
- Chỉ bật lại khi user yêu cầu hoặc bắt đầu session mới.
- Có test case kiểm tra rằng preference này được giữ qua ít nhất 2-3 lượt hội thoại tiếp theo.

---

# 3. Sketch as-is / to-be

| As-is | To-be |
|---|---|
| User yêu cầu: "Tôi không muốn bạn đưa ra các gợi ý tiếp theo sau mỗi phản hồi nữa." | User yêu cầu: "Tôi không muốn bạn đưa ra các gợi ý tiếp theo sau mỗi phản hồi nữa." |
| V-AI trả lời theo hướng đã ghi nhận yêu cầu của user. | V-AI xác nhận rõ: từ các lượt sau trong session này sẽ không hiển thị gợi ý tiếp theo. |
| User hỏi tiếp: "Hướng dẫn mua xe VF9." | User hỏi tiếp: "Hướng dẫn mua xe VF9." |
| V-AI trả lời nội dung hướng dẫn nhưng vẫn hiển thị các gợi ý tiếp theo. | V-AI chỉ trả lời trực tiếp nội dung hướng dẫn mua VF9, không hiển thị suggestion chips/gợi ý tiếp theo. |
| User phát hiện AI không làm đúng điều đã xác nhận, phải correction lại. | User không cần nhắc lại yêu cầu, vì preference đã được áp dụng trong session. |
| Điểm gãy: AI hiểu câu correction ở mức ngôn ngữ nhưng không chuyển thành thay đổi hành vi của UI/response. | Path đã sửa: correction của user được lưu tạm trong session và ảnh hưởng trực tiếp tới cách V-AI phản hồi. |

---

# 4. Finding này sẽ đổi gì trong SPEC

SPEC cần bổ sung requirement để V-AI ghi nhớ preference của user trong session hiện tại.

Cụ thể, khi user yêu cầu không hiển thị các gợi ý tiếp theo sau mỗi phản hồi, V-AI phải tắt suggestion chips trong các lượt trả lời tiếp theo của cùng session và chỉ bật lại khi user yêu cầu hoặc bắt đầu session mới.

SPEC cũng cần có test case kiểm tra hành vi này bằng cách cho user đưa ra preference, hỏi tiếp ít nhất 2-3 lượt, và xác nhận rằng V-AI không còn hiển thị gợi ý tiếp theo.

---

# 5. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể.
- [x] Có đủ 4 paths: Happy, Low-confidence, Failure, Correction đều đã được test với prompt cụ thể và có evidence screenshot đi kèm.
- [x] Finding được viết thành product decision, không chỉ là nhận xét.
- [x] Sketch có as-is và to-be.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.
