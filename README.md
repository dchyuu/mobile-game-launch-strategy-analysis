# Phân Tích Chiến Lược Ra Mắt Mobile Game Trên App Store

## 1. Tổng quan dự án

Dự án này phân tích dữ liệu App Store Games giai đoạn 2008–2019 nhằm hỗ trợ một studio game mobile đưa ra chiến lược ra mắt sản phẩm mới.

Mục tiêu của dự án không phải là trả lời đơn giản rằng **Free game hay Paid game tốt hơn**, mà là xác định:

> Nếu studio chọn chiến lược Free thì cần điều kiện thành công nào?  
> Nếu studio chọn chiến lược Paid thì cần điều kiện thành công nào?

Vì Free và Paid là hai mô hình kinh doanh khác nhau, dự án được chia thành hai hướng phân tích:

- **Free / Viral Strategy**: tập trung vào mở rộng người dùng, độ phổ biến, khả năng viral và giảm rào cản tải game.
- **Paid / Premium Strategy**: tập trung vào chất lượng cảm nhận, khả năng người dùng sẵn sàng trả tiền, chiến lược giá và định vị premium.

---

## 2. Bối cảnh kinh doanh

Một studio game mobile muốn ra mắt game mới trên App Store. Trước khi đầu tư phát triển sản phẩm, studio cần trả lời các câu hỏi:

1. Nên chọn chiến lược Free hay Paid?
2. Nếu chọn Free, genre nào phù hợp để scale user?
3. Nếu chọn Paid, mức giá nào hợp lý?
4. Game/developer nào nên được benchmark?
5. Localization có giúp tăng độ phủ thị trường không?
6. Genre nào còn tiềm năng cho game mới?
7. Chiến lược ra mắt cuối cùng nên là gì?

---

## 3. Dataset

Dataset gồm thông tin các game trên App Store trong giai đoạn 2008–2019.

Các trường dữ liệu chính:

| Cột | Ý nghĩa |
|---|---|
| App ID | Mã định danh ứng dụng |
| Name | Tên game |
| Average User Rating | Điểm đánh giá trung bình |
| User Rating Count | Số lượng lượt đánh giá |
| Price per App (USD) | Giá bán ứng dụng |
| Developer | Nhà phát triển |
| Age Rating | Nhóm tuổi |
| Languages | Ngôn ngữ hỗ trợ |
| Size in Bytes | Dung lượng ứng dụng |
| Primary Genre | Genre chính |
| Genres | Danh sách genre chi tiết |
| Release Date | Ngày phát hành |

---

## 4. Giới hạn dữ liệu

Dataset không có các thông tin quan trọng như:

- Lượt tải thật
- Doanh thu thật
- Retention
- DAU / MAU
- Session time
- In-app purchase
- Ads revenue
- Chi phí marketing
- Nội dung review của người dùng

Vì vậy, dự án sử dụng các proxy metric sau:

| Metric | Ý nghĩa |
|---|---|
| User Rating Count | Proxy cho độ phổ biến |
| Average User Rating | Proxy cho chất lượng cảm nhận |
| Weighted Rating | Rating có trọng số theo số lượt đánh giá |
| Paid Revenue Proxy | Price × User Rating Count |
| Success Score | Kết hợp rating và popularity |

Lưu ý:

`Paid Revenue Proxy` không phải doanh thu thật. Chỉ số này chỉ dùng để so sánh tiềm năng monetization tương đối trong nhóm paid games.

---

## 5. Cấu trúc repository

```text
mobile-game-launch-strategy-analysis/
│
├── README.md
├── BAO_CAO_TOM_TAT.md
│
├── notebooks/
│   ├── free_mobile_game_launch_strategy.ipynb
│   └── paid_mobile_game_launch_strategy.ipynb
│
├── data/
│   └── App Store Games.xlsx
│
├── dashboard/
│   └── mobile_game_strategy_dashboard.pbix
│
└── outputs/
    └── charts/
```

---

## 6. Quy trình phân tích

### Bước 1: Xác định business problem

Ban đầu, bài toán khá rộng:

> Nên chọn genre nào?  
> Nên chọn Free hay Paid?  
> Có nên localization không?  
> Nên benchmark developer nào?

Sau khi điều chỉnh theo góp ý mentor, project được framing lại thành:

> Studio nên chọn chiến lược ra mắt nào: Free/Viral hay Paid/Premium?  
> Với từng chiến lược, điều kiện thành công là gì?

---

### Bước 2: Làm sạch dữ liệu

Các bước xử lý chính:

- Chuẩn hóa tên cột.
- Chuyển dữ liệu ngày tháng về dạng datetime.
- Chuyển rating, rating count, price và size về dạng numeric.
- Xóa duplicate theo App ID.
- Tạo cột release year.
- Quy đổi size từ bytes sang MB.
- Phân loại Free/Paid.
- Tạo số lượng ngôn ngữ hỗ trợ.
- Tách game genre chi tiết từ cột Genres.
- Tạo nhóm giá.
- Tạo giai đoạn phân tích theo 3 năm.

---

### Bước 3: Feature Engineering

Các biến mới được tạo:

| Biến | Công thức / Ý nghĩa |
|---|---|
| Price Type | Free nếu giá = 0, Paid nếu giá > 0 |
| Paid Revenue Proxy | Price × User Rating Count |
| Popularity Log | log(1 + User Rating Count) |
| Success Score | Average Rating × log(1 + User Rating Count) |
| Weighted Rating | Rating trung bình có trọng số theo rating count |
| High Performing App | Game vừa có rating cao vừa có rating count cao |
| Recent Release Ratio | Tỷ lệ game phát hành trong 2017–2019 theo từng genre |

---

## 7. Nội dung phân tích chính

Dự án bao gồm các phần:

1. Top game phổ biến theo từng năm.
2. Top game nổi bật trong giai đoạn 2016–2019.
3. Developer đáng benchmark theo weighted rating.
4. Developer có paid revenue proxy cao.
5. Xu hướng rating, pricing và popularity theo thời gian.
6. So sánh Free vs Paid strategy.
7. Phân tích localization theo language count, genre và price type.
8. Genre evolution theo từng giai đoạn 3 năm.
9. Genre opportunity scoring có bổ sung freshness.
10. Pricing recommendation dựa trên giai đoạn gần nhất 2016–2019.
11. Case study một game benchmark cụ thể.
12. Đề xuất chiến lược cuối cùng.

---

## 8. Key Findings

### Finding 1: Không nên đánh giá thành công chỉ bằng rating

Một game có rating 5 sao nhưng chỉ có vài lượt đánh giá không thể so sánh ngang với game 4.5 sao nhưng có hàng trăm nghìn lượt đánh giá.

Vì vậy, project sử dụng thêm:

- User Rating Count
- Weighted Rating
- Success Score
- High-performing flag

Điều này giúp việc chọn benchmark đáng tin cậy hơn.

---

### Finding 2: Free và Paid là hai chiến lược khác nhau

Free game phù hợp hơn với mục tiêu scale user, tăng reach và giảm rào cản tải game.

Paid game yêu cầu chất lượng cảm nhận cao hơn vì người dùng phải trả tiền trước khi trải nghiệm sản phẩm.

Vì vậy, không nên kết luận:

> Free tốt hơn Paid.

Mà nên kết luận:

> Free và Paid là hai chiến lược khác nhau, phù hợp với hai mục tiêu kinh doanh khác nhau.

---

### Finding 3: Pricing nên dựa trên giai đoạn gần nhất

Giá $0.99 ở năm 2008 không nên được hiểu giống $0.99 ở năm 2019 vì thị trường, hành vi người dùng và mô hình monetization đã thay đổi.

Do đó, recommendation về pricing nên ưu tiên giai đoạn:

> 2016–2019

Giai đoạn này phù hợp hơn để tham khảo cho một game mới.

---

### Finding 4: Genre strategy cần thêm yếu tố freshness

Một genre có độ phổ biến cao trong quá khứ chưa chắc còn là cơ hội tốt cho game mới.

Project bổ sung chỉ số:

> Recent Release Ratio = số game release trong 2017–2019 / tổng số game của genre

Một genre hấp dẫn nên có:

- Demand tốt
- Weighted rating tốt
- Competition không quá cao
- Recent release ratio đủ tốt
- Có benchmark game cụ thể

---

### Finding 5: Localization nên được triển khai theo giai đoạn

Localization có thể liên quan đến khả năng mở rộng thị trường, nhưng không thể kết luận rằng càng nhiều ngôn ngữ thì game chắc chắn càng thành công.

Với Free/Viral game, studio nên bắt đầu với một số ngôn ngữ chính trước.

Với Paid/Premium hoặc game dài hạn có cộng đồng quốc tế, localization có thể đóng vai trò quan trọng hơn.

---

## 9. Đề xuất cuối cùng

### Nếu studio muốn scale user nhanh

Nên chọn **Free / Viral Strategy**.

Hướng triển khai:

- Launch game dạng Free để giảm rào cản tải.
- Ưu tiên genre có demand cao và recent release ratio tốt.
- Benchmark các game high-performing trong cùng genre.
- Bắt đầu localization với các ngôn ngữ quan trọng nhất.
- Mở rộng localization sau khi game có traction.

Chiến lược này phù hợp nếu studio muốn test thị trường nhanh và xây dựng user base.

---

### Nếu studio muốn làm game premium

Có thể chọn **Paid / Premium Strategy**.

Hướng triển khai:

- Chọn genre có weighted rating tốt.
- Benchmark developer có paid revenue proxy cao.
- Dựa vào pricing recent window 2016–2019 để chọn khoảng giá.
- Không nên đặt giá cao nếu chưa có brand hoặc khác biệt rõ ràng.
- Tập trung vào UX, gameplay depth và perceived quality.

Chiến lược này phù hợp nếu studio có concept khác biệt và sản phẩm đủ chất lượng để thuyết phục người dùng trả tiền trước.

---

## 10. Kết luận chính

Với một studio mới, project khuyến nghị:

> Ưu tiên Free / Viral Strategy nếu mục tiêu là test thị trường, scale user và tạo traction nhanh.

Paid / Premium Strategy vẫn có thể phù hợp, nhưng chỉ nên chọn khi studio có:

- Sản phẩm đủ khác biệt
- Chất lượng gameplay tốt
- Nhóm người dùng niche rõ ràng
- Bằng chứng benchmark từ paid games thành công

---

## 11. Công cụ sử dụng

- Python
- Pandas
- NumPy
- Matplotlib
- Google Colab
- Power BI
- GitHub

---

## 12. Cách chạy project

1. Clone repository:

```bash
git clone <repository-url>
```

2. Mở notebook trên Google Colab:

```text
notebooks/free_mobile_game_launch_strategy.ipynb
notebooks/paid_mobile_game_launch_strategy.ipynb
```

3. Upload dataset:

```text
App Store Games.xlsx
```

4. Run toàn bộ notebook từ trên xuống dưới.

5. Mở dashboard Power BI nếu có:

```text
dashboard/mobile_game_strategy_dashboard.pbix
```

---

## 13. Giá trị portfolio

Project này thể hiện các kỹ năng:

- Business problem framing
- Data cleaning
- Feature engineering
- Proxy metric design
- Exploratory data analysis
- Free vs Paid strategy thinking
- Genre opportunity scoring
- Pricing recommendation
- Localization analysis
- Executive reporting
