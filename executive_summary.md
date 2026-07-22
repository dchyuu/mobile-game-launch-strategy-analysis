# Báo Cáo Tóm Tắt  
## Phân Tích Chiến Lược Ra Mắt Mobile Game

### Business Question

Một studio game mobile muốn ra mắt game mới trên App Store. Câu hỏi quan trọng không phải là Free hay Paid tốt hơn, mà là:

> Studio nên chọn chiến lược ra mắt nào để phù hợp với mục tiêu kinh doanh?

Project đánh giá hai hướng chiến lược:

- **Free / Viral Strategy**: tối đa hóa độ phủ, user scale và popularity.
- **Paid / Premium Strategy**: tối đa hóa chất lượng cảm nhận, willingness to pay và định vị premium.

---

## 1. Rating đơn thuần không đủ để đánh giá thành công

Một game rating 5 sao nhưng chỉ có vài lượt đánh giá không thể so sánh ngang với game rating 4.5 sao nhưng có hàng trăm nghìn lượt đánh giá.

Vì vậy, project không chỉ dùng Average Rating mà bổ sung:

- `User Rating Count` làm proxy cho popularity.
- `Weighted Rating` để giảm bias từ game có ít rating.
- `Success Score` để kết hợp rating và popularity.
- `High-performing flag` để xác định game vừa có rating tốt vừa có độ phủ lớn.

Kết luận: benchmark game nên dựa trên cả chất lượng cảm nhận và quy mô tương tác, không chỉ dựa vào rating trung bình.

---

## 2. Free và Paid là hai mô hình khác nhau

Free game phù hợp với mục tiêu tăng reach, mở rộng user base và giảm rào cản tải app. Thành công của Free game nên được đánh giá qua rating count, demand của genre, khả năng scale và localization vừa đủ.

Paid game yêu cầu chất lượng cảm nhận cao hơn vì người dùng phải trả tiền trước khi trải nghiệm. Thành công của Paid game nên được đánh giá qua weighted rating, paid revenue proxy, price range và định vị premium.

Kết luận đúng không phải là:

> Free tốt hơn Paid.

Mà là:

> Free và Paid là hai chiến lược khác nhau, phù hợp với hai mục tiêu kinh doanh khác nhau.

---

## 3. Pricing nên dựa trên giai đoạn gần nhất

Không nên dùng toàn bộ giai đoạn 2008–2019 để đưa ra recommendation về giá, vì thị trường App Store, hành vi người dùng và mô hình monetization đã thay đổi theo thời gian.

Do đó, pricing recommendation nên ưu tiên giai đoạn:

> 2016–2019

Với studio mới, Free là lựa chọn hợp lý hơn nếu mục tiêu là scale user nhanh. Nếu chọn Paid, studio nên benchmark nhóm paid games trong giai đoạn gần nhất và tránh định giá quá cao nếu chưa có brand hoặc điểm khác biệt rõ ràng.

---

## 4. Genre recommendation cần thêm yếu tố freshness

Một genre có popularity cao trong quá khứ chưa chắc còn là cơ hội tốt cho game mới.

Project bổ sung chỉ số:

> Recent Release Ratio = số game release trong 2017–2019 / tổng số game của genre

Một genre đáng cân nhắc cần có:

- Demand đủ lớn.
- Weighted rating tốt.
- Competition không quá cao.
- Recent release ratio đủ tốt.
- Có game benchmark cụ thể.

Kết luận: không nên chọn genre chỉ vì total rating count cao. Cần đánh giá cả sức hút hiện tại và mức độ active của genre trong giai đoạn gần nhất.

---

## 5. Localization nên triển khai theo từng giai đoạn

Localization có thể hỗ trợ mở rộng thị trường, nhưng không thể kết luận rằng càng nhiều ngôn ngữ thì game chắc chắn càng thành công.

Với Free/Viral game, studio nên bắt đầu với một số ngôn ngữ chính để test thị trường trước.

Với Paid/Premium hoặc game dài hạn có cộng đồng quốc tế, localization có thể quan trọng hơn vì sản phẩm cần phục vụ người dùng ở nhiều thị trường.

Kết luận: localization nên được mở rộng theo traction, không nên đầu tư quá rộng ngay từ đầu.

---

# Final Recommendation

## Hướng khuyến nghị chính: Free / Viral Strategy

Với một studio mới chưa có brand mạnh, project khuyến nghị ưu tiên **Free / Viral Strategy**.

Studio nên:

1. Launch game dưới dạng Free để giảm rào cản tải.
2. Chọn genre có demand tốt, weighted rating ổn và recent release ratio cao.
3. Benchmark game high-performing thay vì chỉ benchmark game rating cao.
4. Bắt đầu localization với các ngôn ngữ quan trọng nhất.
5. Theo dõi rating count, weighted rating và success score để đánh giá traction.

Chiến lược này giúp studio test product-market fit nhanh hơn, xây dựng user base và có cơ hội tối ưu monetization sau khi game có traction.

---

## Hướng thay thế: Paid / Premium Strategy

Paid / Premium Strategy chỉ nên chọn nếu studio có:

- Concept game khác biệt.
- Gameplay đủ sâu.
- Chất lượng sản phẩm cao.
- Nhóm người dùng niche rõ ràng.
- Bằng chứng benchmark từ paid games thành công.
- Mức giá hợp lý dựa trên giai đoạn 2016–2019.

Paid strategy có thể tạo định vị premium, nhưng rủi ro cao hơn vì người dùng phải trả tiền trước khi trải nghiệm game.

---

# Kết luận cuối cùng

Project khuyến nghị:

> Studio nên bắt đầu bằng Free / Viral Strategy nếu mục tiêu là test thị trường, scale user và tạo traction nhanh.

Chiến lược cuối cùng nên là:

> Free launch + genre có demand và freshness tốt + benchmark game high-performing + localization theo từng giai đoạn + đánh giá performance bằng rating count, weighted rating và success score.
