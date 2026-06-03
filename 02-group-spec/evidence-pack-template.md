# Evidence Pack — Food / Xanh SM Ngon Chatbot

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm:** Food For You 
**Track:** Food / Food delivery  
**Product/app đã chọn:** Xanh SM Ngon trong ứng dụng Xanh SM  
**Build slice đang nghĩ:** Chatbot hỗ trợ học viên khóa AI thực chiến tại VinUni đặt món trưa qua Xanh SM Ngon khi căng tin quá đông, cần món giao nhanh, còn nóng và ăn kịp trong 1 tiếng nghỉ trưa.

## 2. Self-use evidence

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Trong giờ nghỉ trưa 1 tiếng, căng tin VinUni đông khiến học viên phải xếp hàng lâu hoặc mất thời gian tìm chỗ ăn. | cantin_food.jpg - Ảnh căng tin đông giờ trưa. | Failure | Pain chính là thiếu thời gian ăn, không chỉ là không biết chọn món. |
| Khi đặt món trên Xanh SM Ngon, user vẫn phải tự lướt món/quán và tự đoán món nào giao kịp, còn nóng, dễ ăn nhanh. | xanhsm_ngon.jpg - Màn hình Xanh SM Ngon. | Low-confidence | Chatbot cần ưu tiên ràng buộc thời gian và nhiệt độ món, không chỉ khẩu vị. |

## 3. User / review / social evidence

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| Xanh SM Ngon có hơn 2.000 nhà hàng đối tác tại Hà Nội khi ra mắt. | Thanh Niên / VnExpress. | Học viên tại VinUni có nhiều lựa chọn đặt món quanh khu vực. | Nhiều lựa chọn gây khó quyết định trong giờ nghỉ ngắn. |
| Dịch vụ nhấn mạnh "không ghép đơn", giao thẳng từ nhà hàng đến người dùng để giữ món nóng/tươi. | Green SM Food / Dân trí / VnExpress. | Học viên cần món đến nhanh, còn nóng, ăn kịp trước giờ học chiều. | Nếu món giao chậm hoặc nguội, user mất bữa trưa hoặc vào lớp muộn. |
| Xanh SM Ngon nhấn mạnh ảnh thật, review thật, chất lượng và bảo hiểm đồ ăn. | Green SM Food / App Store merchant listing. | Học viên cần tin nhanh trước khi đặt quán lạ. | User cần chatbot tóm tắt trust signal thay vì tự đọc nhiều card/review. |

Kiểm chứng thêm bằng phỏng vấn nhanh bạn trong lớp:

```text
Nhóm hỏi: Trong 1 tiếng nghỉ trưa ở VinUni, bạn có thường ăn vội vì căng tin đông không?
Dương trả lời: "Tôi thường mang đồ ăn tự nấu ở nhà đi, tuy nhiên điều này khiến tôi mất nhiều thời gian và công sức hơn, tôi thấy rất tuyệt vời nếu có nền tảng hỗ trợ học viên chúng tôi đặt đồ ăn nhanh chóng và phù hợp với túi tiền."

Nhóm hỏi: Khi đặt đồ ăn ở căng tin, bạn quan tâm nhất điều gì: như chọn món, dễ ăn nhanh, giá, hay khẩu vị?
Huy trả lời: "Khi đến căng tin tôi thường quan tâm đến việc chọn món nào ngon và hàng nào ngắn hơn, để kịp ăn trong giờ trưa."
```

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| GrabFood / ShopeeFood | Lọc theo danh mục, khuyến mãi, gần tôi, rating, thời gian giao. | Có ETA/filter nhưng chưa gắn với bối cảnh "chỉ có 1 tiếng nghỉ trưa". | Có, mock 10-15 món/quán gần VinUni. |
| ChatGPT / AI meal planner | Hỏi khẩu vị, ngân sách, ràng buộc rồi đề xuất món. | AI phù hợp để hỏi lại và thu hẹp lựa chọn theo bối cảnh. | Có, dùng chatbot augmentation. |
| Foody / Google Maps review | Dựa vào ảnh, review, rating để tạo niềm tin. | Gợi ý cần lý do ngắn: gần, nóng, dễ ăn nhanh, rating ổn. | Có, mock tag review/ảnh/ETA. |

## 5. Evidence -> Insight

```text
Evidence nổi bật nhất:
Học viên khóa AI thực chiến tại VinUni chỉ có khoảng 1 tiếng nghỉ trưa, trong khi căng tin đông. Xanh SM Ngon có lợi thế giao nhanh, không ghép đơn, giữ món nóng, nhưng user vẫn phải tự chọn món/quán phù hợp với ràng buộc thời gian.

Insight:
Học viên không chỉ cần danh sách món hoặc khuyến mãi.
Họ cần một cách quyết định nhanh món nào giao kịp, còn nóng, dễ ăn trong thời gian ngắn,
vì nếu chọn sai món/quán, họ có thể không kịp ăn hoặc vào lớp muộn.

Opportunity:
Cơ hội là dùng chatbot AI để hỏi 2-3 câu về thời gian còn lại, ngân sách, khẩu vị và mức độ no,
giúp học viên chọn 1 trong 3 món/quán có khả năng giao kịp và ăn nhanh,
trong khi kiểm soát rủi ro gợi ý sai bằng correction và giải thích ETA/trust signal.
```

## 6. Evidence đổi SPEC như thế nào?

- [x] Đổi user chính.
- [x] Đổi pain statement.
- [x] Đổi build slice.
- [x] Đổi Auto/Aug decision.
- [x] Đổi 4 paths.
- [x] Đổi failure mode.
- [ ] Đổi owner/test plan.

Ghi rõ 1-2 thay đổi quan trọng:

```text
Trước evidence, nhóm định build chatbot đặt đồ ăn chung cho mọi người dùng.

Sau evidence, nhóm đổi thành chatbot hỗ trợ đặt món cho học viên khóa AI thực chiến tại VinUni trong giờ nghỉ trưa 1 tiếng, khi căng tin quá đông.

Lý do:
Build slice này hẹp, có user/bối cảnh rõ, demo được trong 3-5 phút. AI decision là hỏi lại nhu cầu và gợi ý 3 món/quán ưu tiên giao kịp, còn nóng, dễ ăn nhanh; failure path là gợi ý món giao không kịp hoặc không phù hợp ràng buộc.
```

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

Những thứ không build trong Day 06:

- Tích hợp API thật của Xanh SM Ngon.
- Cá nhân hóa dài hạn theo lịch sử đặt món.
- Thanh toán, tracking shipper, voucher thật.
- Tối ưu đặt theo nhóm/lớp hoặc gom đơn nhiều học viên.