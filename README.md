# 📦 Shopping Cart Analysis & Case Study

Phân tích dữ liệu bán lẻ để tìm ra mối quan hệ giữa các sản phẩm thường được mua cùng nhau bằng các kỹ thuật **Association Rule Mining** (Apriori). Project triển khai pipeline đầy đủ từ xử lý dữ liệu → phân tích → khai thác luật → báo cáo.

---

## 👥 Thông tin Nhóm
- **Nhóm:** Nhóm 9
- **Thành viên:**
  - Trần Trường Giang
  - Lưu Khoa Bằng
  - Nguyễn Đức Dương
- **Chủ đề:** 7.3.3 – Đánh giá luật theo Lift và giá trị kinh doanh
  - Xếp hạng luật theo Lift
  - Phân loại luật theo Support / Lift / Confidence
  - Đề xuất marketing tương ứng
- **Dataset:** Online Retail (UCI)

---

## 🎯 Mục tiêu
Hiểu hành vi mua sắm của khách hàng, xác định các cặp sản phẩm gắn kết để:
- Tạo combo, gợi ý mua kèm
- Marketing cá nhân hóa
- Tối ưu bố trí hàng hóa
- Thiết kế chiến dịch khuyến mãi

---

## 📝 Quy trình Thực hiện
1. Làm sạch dữ liệu & xử lý giá trị lỗi
2. Xây dựng basket matrix (transaction × product)
3. Khai phá tập mục phổ biến (Frequent itemsets)
4. Sinh luật kết hợp (Association Rules)
5. Trực quan hóa & phân tích insight
6. Đề xuất hành động kinh doanh

---

## 🧹 Tiền xử lý Dữ liệu
**Các bước làm sạch:**
- Loại bỏ sản phẩm rỗng
- Loại bỏ hóa đơn bị hủy (`InvoiceNo` bắt đầu "C")
- Loại bỏ quantity hoặc price âm / không hợp lệ

**Thống kê nhanh:**
- Số giao dịch sau lọc: 397,924
- Số sản phẩm duy nhất: 4,372
- Khách hàng UK: 4,372

---

## 🔍 Áp dụng Apriori
**Tham số sử dụng:**
- `min_support = 0.01`
- `min_Lift = 1.2`
- `max_confident = 0.3`

**Kết quả:**
- Tổng số luật: 218
- Số luật sau khi lọc (Support ≥0.01, Confidence ≥0.3, Lift ≥1.2): 175

---

## 📊 Visualization (Thay bằng ảnh)
### Biểu đồ 1 – Top 10 luật theo Lift
![Top 10 luật theo Lift](![alt text](image.png))

**Giải thích:**
- Các sản phẩm có Lift cao thường được mua cùng nhau nhiều hơn so với ngẫu nhiên.
- Dùng để tạo combo, gợi ý mua kèm, tối ưu layout cửa hàng.

### Biểu đồ 2 – Scatter plot Support vs Confidence
![Support vs Confidence](![alt text](image-1.png))

**Giải thích:**
- **Support cao + Confidence cao:** luật phổ biến, đáng tin cậy → quan trọng để gợi ý chung
- **Lift cao nhưng Support thấp:** luật mạnh nhưng niche, phù hợp chiến dịch marketing nhỏ, cá nhân hóa

---

## 💡 Insight từ Kết quả
1. **Tạo combo sản phẩm từ Lift cao:**
   - Luật: `ROSES REGENCY TEACUP AND SAUCER → GREEN REGENCY TEACUP AND SAUCER`
   - Lift = 14.16, Confidence = 0.73, Support = 0.0388
   - Hành động: Tạo combo 2 sản phẩm, bày cạnh nhau trên kệ.

2. **Gợi ý cá nhân hóa dựa trên Confidence cao:**
   - Luật: `GREEN REGENCY TEACUP AND SAUCER → ROSES REGENCY TEACUP AND SAUCER`
   - Confidence = 0.75, Lift = 14.16, Support = 0.0388
   - Hành động: Gợi ý mua thêm sản phẩm qua app, POS, email.

3. **Nhận diện sản phẩm phổ biến trong giỏ hàng:**
   - Luật: `JUMBO BAG RED RETROSPOT → JUMBO BAG PINK POLKADOT`
   - Support = 0.0436, Lift = 6.31, Confidence = 0.41
   - Hành động: Đảm bảo tồn kho đầy đủ, tránh hết hàng.

4. **Tối ưu bố trí cửa hàng:**
   - Luật: `JUMBO BAG RED RETROSPOT → JUMBO STORAGE BAG SUKI`
   - Lift = 5.75, Confidence = 0.36
   - Hành động: Bày sản phẩm thường mua cùng nhau gần nhau trên kệ.

5. **Chiến dịch marketing kết hợp sản phẩm:**
   - Luật: `LUNCH BAG RED RETROSPOT → LUNCH BAG BLACK SKULL.`
   - Lift = 6.46, Confidence = 0.44, Support = 0.034
   - Hành động: Gửi voucher hoặc email gợi ý combo Lunch Bag Red → Lunch Bag Black.

---

## 📈 Kết luận & Đề xuất Kinh doanh
- **Cross-sell / Upsell:** Dựa vào các luật Lift cao để tạo combo, ưu đãi mua kèm.
- **Tối ưu bố trí hàng hóa:** Bày sản phẩm gắn kết gần nhau để tăng giá trị giỏ hàng.
- **Marketing cá nhân hóa:** Gửi email, notification dựa trên các luật Confidence cao.
- **Quản lý tồn kho:** Đảm bảo các sản phẩm phổ biến có đủ hàng.
- **Chiến dịch niche products:** Luật Lift cao nhưng Support thấp → marketing nhỏ, targeted campaign.

---

## 📂 Project Structure
```text
shopping_cart_analysis/
├── data/
│   ├── raw/
│   │   └── online_retail.csv
│   └── processed/
│       ├── cleaned_uk_data.csv
│       ├── basket_bool.parquet
│       └── rules_apriori_filtered.csv
├── notebooks/
│   ├── preprocessing_and_eda.ipynb
│   ├── basket_preparation.ipynb
│   ├── apriori_modelling.ipynb
│   └── runs/
├── src/
│   └── apriori_library.py
├── run_papermill.py
├── requirements.txt
└── README.md
