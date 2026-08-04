# Phân Tích Chiến Lược Ra Mắt Mobile Game Trên App Store

## Tổng quan dự án

Dự án phân tích dữ liệu **App Store Games giai đoạn 2008–2019** nhằm hỗ trợ một studio mobile game lựa chọn chiến lược ra mắt sản phẩm mới.

Thay vì kết luận đơn giản rằng **Free game tốt hơn Paid game** hoặc ngược lại, dự án tách bài toán thành hai hướng:

- **Free / Viral Strategy:** tập trung vào mở rộng tập người dùng, tăng độ phổ biến, khả năng viral và giảm rào cản tải game.
- **Paid / Premium Strategy:** tập trung vào chất lượng cảm nhận, khả năng người dùng sẵn sàng trả tiền, chiến lược giá và định vị premium.

> Mục tiêu chính: xác định điều kiện thành công của từng chiến lược và đưa ra khuyến nghị phù hợp với mục tiêu kinh doanh của studio.

---

## Xem kết quả dự án

- [Báo cáo phân tích hoàn chỉnh](./bao_cao_phan_tich_du_lieu.html)  
  Báo cáo HTML đã nhúng biểu đồ. Để xem đầy đủ, hãy tải file xuống và mở bằng trình duyệt.

- [Notebook phân tích Free / Viral Strategy](./free_mobile_game_launch_strategy.ipynb)

- [Notebook phân tích Paid / Premium Strategy](./paid_mobile_game_launch_strategy.ipynb)

---

## Bối cảnh kinh doanh

Một studio mobile game đang chuẩn bị ra mắt sản phẩm mới trên App Store và cần trả lời các câu hỏi:

1. Khi nào nên chọn chiến lược Free / Viral?
2. Khi nào nên chọn chiến lược Paid / Premium?
3. Genre nào có tín hiệu phù hợp với từng chiến lược?
4. Developer và game nào nên được sử dụng làm benchmark?
5. Mức giá nào hợp lý cho paid game?
6. Số lượng ngôn ngữ hỗ trợ có liên hệ như thế nào với mức độ phổ biến?
7. Genre nào thể hiện cơ hội tương đối khi xét đồng thời demand, quality, competition và freshness?

---

## Dataset

Dữ liệu sử dụng trong dự án là **App Store Games Dataset**, bao gồm thông tin về khoảng 17.000 ứng dụng trong giai đoạn 2008–2019.

### Tải dữ liệu

Dataset không được lưu trực tiếp trong GitHub repository. File dữ liệu được lưu trong thư mục Google Drive:

**[Mở thư mục dataset trên Google Drive](https://drive.google.com/drive/folders/1NrvyT_tMArcoZvI_sEgPLclD4Vw0iCBq?usp=sharing)**

Tên file dữ liệu:

```text
App Store Games.xlsx
```

### Các trường dữ liệu chính

| Cột | Ý nghĩa |
|---|---|
| App ID | Mã định danh ứng dụng |
| Name | Tên game |
| Average User Rating | Điểm đánh giá trung bình |
| User Rating Count | Số lượt đánh giá |
| Price per App (USD) | Giá bán ứng dụng |
| Developer | Nhà phát triển |
| Age Rating | Nhóm tuổi |
| Languages | Danh sách ngôn ngữ hỗ trợ |
| Size in Bytes | Dung lượng ứng dụng |
| Primary Genre | Genre chính |
| Genres | Danh sách genre chi tiết |
| Release Date | Ngày phát hành |

---

## Phạm vi và giới hạn dữ liệu

Dataset không có các chỉ số vận hành và tài chính quan trọng như:

- Lượt tải thực tế
- Doanh thu thực tế
- Retention
- DAU / MAU
- Session time
- In-app purchase
- Ads revenue
- Chi phí marketing
- Nội dung review của người dùng

Do đó, dự án sử dụng một số proxy metric:

| Metric | Vai trò trong phân tích |
|---|---|
| User Rating Count | Proxy cho mức độ phổ biến |
| Average User Rating | Proxy cho chất lượng cảm nhận |
| Weighted Rating | Rating có trọng số theo số lượt đánh giá |
| Popularity Log | Giảm ảnh hưởng của các giá trị rating count quá lớn |
| Success Score | Kết hợp rating và popularity |
| Paid Revenue Proxy | Price × User Rating Count |

> `Paid Revenue Proxy` không phải doanh thu thực tế. Chỉ số này chỉ được sử dụng để so sánh tương đối giữa các paid game trong dataset.

Dataset kết thúc vào năm 2019. Vì vậy, kết quả phản ánh mô hình lịch sử của App Store Games và chủ yếu được dùng để minh họa quy trình ra quyết định dựa trên dữ liệu. Trước khi áp dụng vào thị trường hiện tại, cần đối chiếu thêm dữ liệu mới về acquisition cost, retention, in-app purchase và xu hướng genre.

---

## Quy trình phân tích

### 1. Business understanding

Bài toán được framing lại từ nhiều câu hỏi rời rạc thành hai nhánh chiến lược:

```text
Free / Viral Strategy
        hoặc
Paid / Premium Strategy
```

Mỗi nhánh sử dụng tiêu chí đánh giá và recommendation riêng.

### 2. Data cleaning

Các bước xử lý chính:

- Chuẩn hóa tên cột.
- Chuyển ngày phát hành sang định dạng datetime.
- Chuyển rating, rating count, price và size sang numeric.
- Xóa duplicate theo App ID.
- Tạo release year.
- Quy đổi dung lượng từ bytes sang MB.
- Phân loại ứng dụng thành Free và Paid.
- Tạo số lượng ngôn ngữ hỗ trợ.
- Tách genre chi tiết.
- Tạo nhóm giá và giai đoạn phân tích.

### 3. Feature engineering

| Biến | Công thức hoặc ý nghĩa |
|---|---|
| Price Type | Free nếu giá = 0; Paid nếu giá > 0 |
| Paid Revenue Proxy | Price × User Rating Count |
| Popularity Log | log(1 + User Rating Count) |
| Success Score | Average Rating × log(1 + User Rating Count) |
| Weighted Rating | Rating có điều chỉnh theo số lượt đánh giá |
| High-performing App | Game đồng thời có rating và rating count cao |
| Recent Release Ratio | Tỷ lệ game phát hành trong 2017–2019 của từng genre |

### 4. Phân tích chuyên sâu

- Xu hướng số lượng game, rating, pricing và popularity theo thời gian.
- So sánh Free và Paid theo mục tiêu kinh doanh.
- Phân tích genre theo demand, quality, competition và freshness.
- Xác định developer và game phù hợp để benchmark.
- Phân tích localization theo số ngôn ngữ, genre và price type.
- Đánh giá khoảng giá paid game trong giai đoạn gần nhất 2016–2019.
- Xây dựng recommendation riêng cho Free / Viral và Paid / Premium.

---

## Key findings

### 1. Rating không đủ để đánh giá thành công

Một game có rating cao nhưng chỉ có vài lượt đánh giá không thể được xem là benchmark tương đương với một game có rating tốt và hàng nghìn lượt đánh giá.

Vì vậy, dự án đánh giá đồng thời:

- Average User Rating
- User Rating Count
- Weighted Rating
- Success Score
- High-performing flag

### 2. Free và Paid phục vụ hai mục tiêu khác nhau

- **Free game** phù hợp hơn với mục tiêu giảm rào cản tải, thử nghiệm thị trường và mở rộng user base.
- **Paid game** yêu cầu perceived quality cao hơn vì người dùng phải thanh toán trước khi trải nghiệm.

Do đó, dự án không kết luận mô hình nào tốt hơn tuyệt đối mà xác định điều kiện để từng mô hình có khả năng thành công.

### 3. Pricing cần ưu tiên dữ liệu gần thời điểm hiện tại của dataset

Recommendation về giá được xây dựng chủ yếu từ giai đoạn **2016–2019**, vì mức giá ở những năm đầu của App Store không còn đại diện tốt cho hành vi thị trường ở giai đoạn sau.

### 4. Genre opportunity cần xét thêm freshness

Popularity trong quá khứ không đủ để kết luận một genre còn hấp dẫn cho sản phẩm mới.

Dự án bổ sung `Recent Release Ratio` để đánh giá xem một genre có còn được developer tiếp tục phát hành sản phẩm trong giai đoạn 2017–2019 hay không.

### 5. Localization nên được triển khai theo giai đoạn

Số lượng ngôn ngữ hỗ trợ có thể liên hệ với khả năng tiếp cận thị trường, nhưng dữ liệu không đủ để kết luận quan hệ nhân quả.

Recommendation phù hợp là:

1. Ra mắt với nhóm ngôn ngữ ưu tiên.
2. Đo traction và phản hồi người dùng.
3. Mở rộng localization theo thị trường có tín hiệu tốt.

---

## Business recommendations

### Free / Viral Strategy

Phù hợp khi studio muốn:

- Thử nghiệm thị trường nhanh.
- Giảm rào cản tải game.
- Mở rộng user base.
- Tạo traction trước khi tối ưu monetization.

Hướng triển khai:

- Chọn genre có demand và recent release ratio tốt.
- Benchmark các high-performing game trong cùng genre.
- Ra mắt với một số ngôn ngữ ưu tiên.
- Mở rộng localization sau khi có dữ liệu traction.
- Theo dõi thêm retention, acquisition cost và monetization sau launch.

### Paid / Premium Strategy

Phù hợp khi studio có:

- Concept khác biệt.
- Gameplay depth tốt.
- Nhóm người dùng niche rõ ràng.
- Chất lượng sản phẩm đủ để thuyết phục người dùng trả tiền trước.

Hướng triển khai:

- Chọn genre có weighted rating tốt.
- Benchmark developer có tín hiệu paid monetization tương đối cao.
- Tham khảo price band trong giai đoạn 2016–2019.
- Tránh mức giá quá cao nếu studio chưa có thương hiệu hoặc khác biệt rõ ràng.
- Tập trung vào UX, perceived quality và giá trị trải nghiệm.

### Khuyến nghị tổng thể

> Với một studio mới muốn test thị trường và tạo traction nhanh, Free / Viral Strategy là lựa chọn có mức rủi ro ban đầu thấp hơn.

Paid / Premium Strategy vẫn phù hợp khi studio có sản phẩm đủ khác biệt, chất lượng tốt và nhóm khách hàng mục tiêu rõ ràng.

---

## Cấu trúc repository

```text
mobile-game-launch-strategy-analysis/
│
├── LICENSE
├── README.md
├── bao_cao_phan_tich_du_lieu.html
├── free_mobile_game_launch_strategy.ipynb
└── paid_mobile_game_launch_strategy.ipynb
```

Dataset được lưu bên ngoài repository trên Google Drive để giữ repository gọn nhẹ.

---

## Cách chạy project

### Cách 1: Google Colab

1. Tải file `App Store Games.xlsx` từ Google Drive.
2. Mở notebook cần chạy trên GitHub.
3. Chọn **Open in Colab** hoặc tải notebook lên Google Colab.
4. Upload file Excel vào Colab khi notebook yêu cầu.
5. Chạy lần lượt toàn bộ cell.

### Cách 2: Jupyter Notebook trên máy

1. Clone repository:

```bash
git clone <repository-url>
cd mobile-game-launch-strategy-analysis
```

2. Tải `App Store Games.xlsx` từ Google Drive và đặt trong thư mục project:

```text
mobile-game-launch-strategy-analysis/
├── App Store Games.xlsx
├── free_mobile_game_launch_strategy.ipynb
└── paid_mobile_game_launch_strategy.ipynb
```

3. Cài các thư viện cần thiết:

```bash
pip install pandas numpy matplotlib openpyxl jupyter
```

4. Khởi động Jupyter Notebook:

```bash
jupyter notebook
```

5. Mở từng notebook và chọn **Run All**.

> Trường hợp notebook sử dụng đường dẫn dữ liệu khác, hãy cập nhật biến đường dẫn file về `App Store Games.xlsx`.

---

## Công cụ sử dụng

- Python
- Pandas
- NumPy
- Matplotlib
- Google Colab
- Jupyter Notebook
- GitHub

---

## License

Project được phát hành theo giấy phép trong file [LICENSE](./LICENSE).
