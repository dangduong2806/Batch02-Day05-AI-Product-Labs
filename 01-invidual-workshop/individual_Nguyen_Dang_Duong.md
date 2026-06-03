# App Teardown — V-App / V-AI

## 0. Thông tin chung

**Product:** V-App  
**AI feature:** V-AI  
**Task được test:**  
> Ví dụ: Hỏi V-AI về một tác vụ trong app, như tìm tính năng, hướng dẫn thao tác, gợi ý theo ngữ cảnh.

**User persona:**  
> Ví dụ: Người dùng mới, chưa quen flow trong V-App.

**Product promise:**  
> V-AI hứa sẽ giúp user bằng cách: ...

**Evidence đã thu thập:**
- Screenshot: `...`
- Prompt/input đã thử: `...`
- Hành vi quan sát được: `...`
- Quote từ app nếu có: `...`

---

# 1. Four Paths Overview

| Path | Test prompt / Trigger | AI response hiện tại | User thấy gì? | Vấn đề chính | Product decision |
|---|---|---|---|---|---|
| Happy | `...` | `...` | `...` | Không / ít vấn đề | Giữ flow hiện tại hoặc làm rõ thêm |
| Low-confidence | `...` | `...` | `...` | AI không chắc nhưng vẫn trả lời như chắc | Thêm hỏi lại / show options |
| Failure | `...` | `...` | `...` | AI sai nhưng user không biết cách sửa | Thêm fallback / recovery |
| Correction | `...` | `...` | `...` | User sửa nhưng context không được cập nhật | Lưu correction vào state/log |

---

# 2. Path 1 — Happy Path

## 2.1 Trigger

User nhập:

```text
...