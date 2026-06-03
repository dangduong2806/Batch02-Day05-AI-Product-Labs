# Thin SPEC Cuối Day 05 — Xanh SM Ngon Lunch Chatbot

Thin SPEC không phải PRD đầy đủ. Đây là bản cam kết đủ rõ để sáng Day 06 nhóm build ngay.

## 1. Track, product/app và user

**Track:** Food / Food delivery  
**Product/app thật:** Xanh SM Ngon trong ứng dụng Xanh SM  
**User cụ thể:** Học viên khóa AI thực chiến đang học tại VinUni, có 1 tiếng nghỉ trưa, cần ăn nhanh khi căng tin quá đông.  
**Nhóm có phải user thật không? Nếu không, khác ở đâu?** Có. Nhóm đang ở đúng bối cảnh học tập, có lịch nghỉ trưa ngắn và có thể quan sát trực tiếp tình trạng căng tin.

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Căng tin VinUni đông vào giờ trưa, trong khi học viên chỉ có khoảng 1 tiếng nghỉ. | cantin_food.jpg - Ảnh căng tin đông giờ trưa. | User cần ăn nhanh, không mất thời gian xếp hàng. | Tập trung vào use case đặt món trưa thay thế căng tin. |
| Xanh SM Ngon nhấn mạnh giao nhanh, không ghép đơn, giữ món nóng/tươi. | Green SM Food / Dân trí / VnExpress. | User cần món đến kịp, còn nóng và ăn được trước giờ học chiều. | Gợi ý phải ưu tiên ETA, độ nóng, độ dễ ăn nhanh. |
| Khi đặt món, user vẫn phải tự lướt danh sách/search/filter và tự đoán món nào phù hợp thời gian nghỉ. | xanhsm_ngon.jpg - Màn hình Xanh SM Ngon. | Pain nằm ở quyết định nhanh dưới áp lực thời gian. | Chatbot hỏi 2-3 câu rồi gợi ý 3 món/quán phù hợp. |

## 3. Pain statement

```text
Học viên khóa AI thực chiến tại VinUni đang gặp khó ở bước ăn trưa trong 1 tiếng nghỉ,
vì căng tin quá đông và nếu đặt món thì phải tự chọn món/quán có thể giao kịp, còn nóng, dễ ăn nhanh,
dẫn tới mất thời gian, ăn vội, bỏ bữa hoặc vào lớp chiều muộn.
Bằng chứng chính là observation tại VinUni và nguồn public về promise giao nhanh/không ghép đơn/giữ món nóng của Xanh SM Ngon.
```

## 4. Build slice

```text
Cho học viên khóa AI thực chiến tại VinUni đang có 1 tiếng nghỉ trưa và căng tin quá đông,
prototype sẽ dùng chatbot AI để hỏi 2-3 câu về thời gian còn lại, ngân sách, khẩu vị và mức độ no,
tạo ra 3 gợi ý món/quán trên Xanh SM Ngon kèm lý do chọn theo ETA, độ nóng, độ dễ ăn nhanh,
và xử lý failure mode gợi ý món giao không kịp hoặc không đúng ràng buộc bằng correction và giải thích tiêu chí gợi ý.
```

## 5. Auto/Aug decision

Chọn một:

- [x] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.

**Lý do chọn:** Đặt món trong giờ nghỉ trưa có ràng buộc cá nhân và thời gian rõ. AI nên hỗ trợ hỏi lại, thu hẹp lựa chọn và gợi ý món phù hợp; user vẫn là người quyết định đặt.  
**Human role:** decider / rescuer

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| Happy | User nhập "mình có 1 tiếng nghỉ, căng tin đông, cần món nóng dưới 80k"; AI gợi ý 3 món/quán giao kịp và nêu lý do. |
| Low-confidence | User nói "ăn gì nhanh cũng được"; AI hỏi lại tối đa 3 câu: còn bao nhiêu phút, ngân sách, muốn ăn no hay ăn nhẹ. |
| Failure | AI gợi ý món có ETA quá lâu hoặc món dễ nguội/khó ăn nhanh; prototype cho thấy user phát hiện và phản hồi. |
| Correction | User sửa "chỉ còn 35 phút, không ăn cay"; AI cập nhật gợi ý sang món gần hơn, dễ ăn hơn và giải thích thay đổi. |

## 7. Failure mode nguy hiểm nhất

```text
Nếu học viên chỉ còn 35-45 phút nghỉ trưa và cần món nóng ăn nhanh,
AI có thể gợi ý món/quán có ETA quá lâu, dễ nguội hoặc không phù hợp ngân sách/khẩu vị,
hậu quả là user không kịp ăn, vào lớp muộn hoặc mất niềm tin vào chatbot.
Prototype sẽ xử lý bằng ask again, cho sửa tiêu chí, show ETA/độ nóng/độ dễ ăn nhanh và fallback sang món gần hơn hoặc món sẵn nhanh hơn.
Owner kiểm thử path này là [tên thành viên phụ trách test].
```

## 8. Owner plan cho sáng Day 06

