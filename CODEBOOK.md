## Bộ dữ liệu dự đoán khả năng sinh lời của phim điện ảnh

### **Thông tin chung**
* **Tên bộ dữ liệu:** Movie profitability prediction dataset.
* **Mô tả:** Bộ dữ liệu có cấu trúc dạng bảng, chứa các đặc trưng liên quan đến tài chính, thể loại, thông tin phát hành và thành phần sản xuất của các bộ phim nhằm mục đích huấn luyện mô hình dự đoán khả năng sinh lời (Classification).
* **Nguồn dữ liệu gốc:** Tích hợp từ cơ sở dữ liệu IMDb và TMDB thông qua API.
* **Phạm vi thu thập dữ liệu:** 
  * **Điều kiện lọc:** titleType = 'movie', numVotes >= 5000 trên IMDb
  * **Giai đoạn:** Phim phát hành trong giai đoạn 2015 - 2025
* **Cấu trúc lưu trữ:** Dữ liệu đã làm sạch và tiền xử lý được chia thành 2 tập (Split ratio: ~80/20):
  * Tập train: movie_train.csv (1774 bản ghi)
  * Tập test: movie_test.csv (444 bản ghi)
* **Số lượng đặc trưng:** 52 biến độc lập + 1 biến mục tiêu.

### **Data Dictionary**

| Tên cột / Nhóm cột | Kiểu dữ liệu | Miền giá trị | Mô tả chi tiết |
| :--- | :--- | :--- | :--- |
| profitable *(Target)* | int64 | 0 hoặc 1 | Biến mục tiêu: Phân loại doanh thu phim. <br>1: Có lãi. <br>0: Không lãi. |
| runtimeMinutes | float64 | Giá trị thực | Thời lượng của bộ phim. Đã được chuẩn hóa. |
| release_year | float64 | Giá trị thực | Năm phát hành của bộ phim. Đã được chuẩn hóa. |
| budget_4root | float64 | Giá trị thực | Ngân sách sản xuất phim. Đã được biến đổi căn bậc 4 và chuẩn hóa. |
| keywords_count_sqrt | float64 | Giá trị thực | Số lượng từ khóa gắn với bộ phim. Đã biến đổi căn bậc 2 và chuẩn hóa. |
| keywords_freq_sum_sqrt | float64 | Giá trị thực | Tổng tần suất xuất hiện của các từ khóa trong kho dữ liệu. Đã biến đổi căn bậc 2 và chuẩn hóa. |
| keywords_freq_max | float64 | Giá trị thực | Tần suất xuất hiện cao nhất của một từ khóa trong phim. Đã chuẩn hóa. |
| production_companies_count_log | float64 | Giá trị thực | Số lượng công ty tham gia sản xuất. Đã biến đổi Logarit và chuẩn hóa. |
| production_companies_freq_sum_sqrt | float64 | Giá trị thực | Tổng tần suất xuất hiện của các công ty sản xuất. Đã biến đổi căn bậc 2 và chuẩn hóa. |
| production_companies_freq_max_sqrt | float64 | Giá trị thực | Tần suất lớn nhất của một công ty sản xuất trong dự án. Đã biến đổi căn bậc 2 và chuẩn hóa. |
| has_us_cert | int64 | 0 hoặc 1 | Biến flag xác định phim có được hệ thống MPAA của Mỹ phân loại độ tuổi hay không (1 = Có, 0 = Không). |
| cert_[X]<br>*(4 cột)* | int64 | 0 hoặc 1 | Nhãn phân loại độ tuổi. Gồm các cột: cert_G_PG, cert_PG-13, cert_R_NC-17, và cert_NR (Không phân loại). |
| lang_[X]<br>*(4 cột)* | int64 | 0 hoặc 1 | Ngôn ngữ gốc của phim. Gồm: lang_en, lang_fr, lang_hi, lang_other |
| country_[X]<br>*(5 cột)* | int64 | 0 hoặc 1 | Quốc gia sản xuất chính. Gồm: country_US, country_GB, country_FR, country_IN và country_other. |
| month_[X]<br>*(12 cột)* | int64 | 0 hoặc 1 | Tháng phát hành phim (từ month_1 đến month_12). |
| genre_[X]<br>*(17 cột)* | int64 | 0 hoặc 1 | Thể loại phim. Một bộ phim có thể thuộc nhiều thể loại cùng lúc. Gồm 17 cột: genre_Action, genre_Comedy, genre_Drama, genre_Horror,... |