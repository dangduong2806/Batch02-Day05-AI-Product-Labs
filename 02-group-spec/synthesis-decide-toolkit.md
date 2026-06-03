# Toolkit — Từ Evidence Đến Build Slice

Nhóm: **Food For You**  
Track: **Food / Food delivery**  
Nền tảng thử nghiệm: **Xanh SM Ngon trong ứng dụng Xanh SM**

Mục tiêu của file này là chốt build slice đủ nhỏ cho Day 06, dựa trên evidence pack và thin SPEC.

## 1. Gom evidence thành cụm

Gom theo **workflow/pain**, không gom theo tên feature.

| Cụm evidence | Bằng chứng chính | Pain học được |
|---|---|---|
| Giờ nghỉ trưa ngắn, căng tin đông | `cantin_food.jpg`; observation tại VinUni; phỏng vấn Huy về việc chọn hàng ngắn để kịp ăn trưa. | Học viên không chỉ cần món ngon, mà cần ăn kịp trong 1 tiếng nghỉ. |
| Đặt món vẫn mất thời gian quyết định | `xanhsm_ngon.jpg`; user phải tự lướt món/quán/search/filter. | Khi đang vội, nhiều lựa chọn làm user chậm quyết định. |
| Cần món giao nhanh, còn nóng, đáng tin | Promise công khai của Xanh SM Ngon: giao nhanh, không ghép đơn, giữ món nóng/tươi, ảnh/review thật. | Gợi ý món phải ưu tiên ETA, độ nóng, độ dễ ăn nhanh và trust signal. |
| User cần hỗ trợ theo bối cảnh VinUni | Phỏng vấn Dương: muốn nền tảng hỗ trợ đặt đồ ăn nhanh và phù hợp túi tiền. | Chatbot cần hỏi đúng ràng buộc: còn bao nhiêu phút, ngân sách, khẩu vị, mức độ no. |

## 2. Viết insight

```text
Học viên khóa AI thực chiến tại VinUni không chỉ cần danh sách món ăn hoặc khuyến mãi.
Họ thật ra cần hỗ trợ ra quyết định ăn trưa thật nhanh và đáng tin,
vì chỉ có khoảng 1 tiếng nghỉ, căng tin đông, và nếu chọn sai món/quán thì có thể không kịp ăn hoặc vào lớp muộn.
```

## 3. Viết opportunity

```text
Cơ hội là dùng chatbot AI để hỏi 2-3 câu về thời gian còn lại, ngân sách, khẩu vị và mức độ no,
giúp học viên chọn 1 trong 3 món/quán có khả năng giao kịp, còn nóng và dễ ăn nhanh,
trong khi vẫn kiểm soát rủi ro gợi ý sai bằng correction, ETA/trust signal và fallback sang món gần hơn hoặc món sẵn nhanh hơn.
```

## 4. Chọn build slice

| Câu hỏi | Quyết định của nhóm |
|---|---|
| User cụ thể chưa? | Có: học viên khóa AI thực chiến tại VinUni, có 1 tiếng nghỉ trưa, căng tin đông. |
| Task đủ hẹp chưa? | Có: chatbot hỏi nhu cầu và gợi ý 3 món/quán để đặt trưa, không build toàn bộ app đặt đồ ăn. |
| AI decision rõ chưa? | Có: AI phân loại ràng buộc và xếp hạng món theo ETA, độ nóng, độ dễ ăn nhanh, ngân sách, khẩu vị. |
| Failure path rõ chưa? | Có: AI gợi ý món giao không kịp, dễ nguội hoặc sai ràng buộc user. |
| Có evidence không? | Có: ảnh/observation căng tin, screenshot Xanh SM Ngon, nguồn public, phỏng vấn nhanh trong lớp. |

Build slice chốt:

```text
Cho học viên khóa AI thực chiến tại VinUni đang có 1 tiếng nghỉ trưa và căng tin quá đông,
prototype dùng chatbot AI để hỏi 2-3 câu về thời gian còn lại, ngân sách, khẩu vị và mức độ no,
tạo ra 3 gợi ý món/quán trên Xanh SM Ngon kèm lý do chọn theo ETA, độ nóng, độ dễ ăn nhanh,
và xử lý failure mode gợi ý món giao không kịp hoặc không đúng ràng buộc bằng correction và giải thích tiêu chí gợi ý.
```

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Quyết định |
|---|---|
| Ý tưởng ban đầu là chatbot đặt đồ ăn chung | Giảm scope xuống một flow: đặt bữa trưa cho học viên VinUni trong 1 tiếng nghỉ. |
| User đã rõ và pain có evidence | Giữ hướng build chatbot, không quay lại research rộng. |
| AI không nên tự đặt món | Chọn **Augmentation**: AI gợi ý, user quyết cuối. |
| Rủi ro chính là gợi ý sai thời gian/món | Bắt buộc có correction path và giải thích ETA/trust signal. |
| Không đủ thời gian tích hợp thật | Dùng mock data 10-15 món/quán gần VinUni, đưa API/thanh toán/tracking vào backlog. |

## 6. Four paths cần demo

| Path | Prototype phải thể hiện |
|---|---|
| Happy | User nhập "mình có 1 tiếng nghỉ, căng tin đông, cần món nóng dưới 80k"; AI gợi ý 3 món/quán giao kịp và nêu lý do. |
| Low-confidence | User nói "ăn gì nhanh cũng được"; AI hỏi lại tối đa 3 câu: còn bao nhiêu phút, ngân sách, muốn ăn no hay ăn nhẹ. |
| Failure | AI gợi ý món có ETA quá lâu hoặc món dễ nguội/khó ăn nhanh; user phát hiện và phản hồi. |
| Correction | User sửa "chỉ còn 35 phút, không ăn cay"; AI cập nhật gợi ý sang món gần hơn, dễ ăn hơn và giải thích thay đổi. |

## 7. Câu chốt cuối

```text
Dựa trên evidence về căng tin VinUni đông giờ trưa, thời gian nghỉ chỉ khoảng 1 tiếng và promise giao nhanh/không ghép đơn của Xanh SM Ngon,
nhóm sẽ build chatbot hỗ trợ đặt món,
cho học viên khóa AI thực chiến tại VinUni,
để giải quyết pain cần đồ ăn nhanh, còn nóng, ăn kịp trước giờ học chiều,
bằng cách AI hỏi 2-3 câu rồi gợi ý 3 món/quán phù hợp theo ETA, độ nóng, độ dễ ăn và ngân sách,
và sẽ test failure path AI gợi ý món giao không kịp hoặc không đúng ràng buộc của user.
```

## 8. Backlog

Những thứ **không build trong Day 06**:

- Tích hợp API thật của Xanh SM Ngon.
- Thanh toán, tracking shipper, voucher thật.
- Cá nhân hóa dài hạn theo lịch sử đặt món.
- Tối ưu đặt theo nhóm/lớp hoặc gom đơn nhiều học viên.
- Dự đoán thời gian chuẩn bị món theo dữ liệu real-time của nhà hàng.