# Movie Profitability Prediction Dataset

## Motivation

1. **For what purpose was the dataset created?**

    Dataset được tạo ra nhằm phục vụ bài toán phân loại nhị phân: dự đoán khả năng sinh lời của phim dựa trên các đặc trưng có thể thu thập được sau khi hoàn tất sản xuất nhưng trước thời điểm công chiếu (ngân sách, thể loại, nhà sản xuất, v.v.). Mục tiêu là hỗ trợ các nhà phát hành phim đánh giá rủi ro tài chính một cách khách quan và khoa học hơn, từ đó đưa ra quyết định đầu tư hợp lý cho giai đoạn phân phối và khai thác phim tại rạp.


2. **Who created this dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)?**

    Dataset được tạo bởi nhóm sinh viên năm 2 Nguyễn Lê Bảo và Nguyễn Xuân Cường trong khuôn khổ đồ án môn học Tiền xử lý và xây dựng bộ dữ liệu (DS108) tại Trường Đại học Công nghệ Thông tin. 


3. **Who funded the creation of the dataset?**

    Không có nguồn tài trợ bên ngoài. Dataset được xây dựng bằng cách thu thập dữ liệu công khai từ TMDB API và IMDb.


4. **Any other comments?**

    Không.




## Composition


1. **What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)?**

    Mỗi instance đại diện cho một bộ phim điện ảnh phát hành trên rạp trong giai đoạn 2015-2025, có đầy đủ dữ liệu ngân sách và doanh thu. Mỗi instance bao gồm các thuộc tính mô tả bộ phim (ngân sách, thể loại, thời lượng, thời gian phát hành, ngôn ngữ, quốc gia sản xuất, nhà sản xuất, từ khóa, phân loại nội dung) và nhãn nhị phân profitable cho biết phim có đạt tỷ lệ doanh thu/ngân sách ≥ 2.5x hay không.


2. **How many instances are there in total (of each type, if appropriate)?**

    Tập dữ liệu gồm 2218 phim. Tỷ lệ nhãn xấp xỉ 60% không sinh lời (0) và 40% sinh lời (1).

    Tập dữ liệu được chia theo tỷ lệ 80/20 (stratified) thành:
    - movie_train.csv: 1,774 phim
    - movie_test.csv: 444 phim


3. **Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set?**

    Đây là một tập con của toàn bộ phim phát hành trên toàn thế giới giai đoạn 2015-2025. Tập con này **không đại diện** cho toàn bộ thị trường: do yêu cầu phải có đầy đủ dữ liệu tài chính (budget và revenue), tập dữ liệu có xu hướng nghiêng về phim phát hành rộng rãi trên rạp, ngân sách trung bình-lớn, chủ yếu Anh ngữ (Hollywood). Phim từ các thị trường nhỏ hơn và một số thể loại (như phim tài liệu) bị thiếu hụt đáng kể.


4. **What data does each instance consist of?**

    Mỗi điểm dữ liệu bao gồm các đặc trưng (thuộc tính đã được trích xuất và xử lý, không phải dữ liệu thô). Cụ thể, mỗi điểm dữ liệu đại diện cho một bộ phim duy nhất và chứa nhiều đặc trưng khác nhau được thiết kế nhằm dự đoán khả năng sinh lời của bộ phim đó. Dưới đây là data dictionary chi tiết mô tả toàn bộ các đặc trưng cho mỗi điểm dữ liệu:

    
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


5. **Is there a label or target associated with each instance? If so, please provide a description.**

    Nhãn mục tiêu là biến nhị phân profitable, được tính theo công thức:

    $$\text{profitable} =
    \begin{cases}
        1,        & \quad \text{nếu } \dfrac{\text{revenue}}{\text{budget}} \ge 2.5\\
        0,        & \quad \text{ngược lại}
    \end{cases}
    $$


6. **Is any information missing from individual instances?**

    Không. Không có thông tin nào bị thiếu.

    Bất kỳ điểm dữ liệu nào trong tập dữ liệu thô ban đầu bị thiếu thông tin đều đã bị loại bỏ hoặc xử lý trong quá trình làm sạch để đảm bảo chất lượng dữ liệu. Do đó, toàn bộ các điểm dữ liệu trong tập dữ liệu cuối cùng này đều là các bản ghi hoàn chỉnh cho mọi đặc trưng.


7. **Are relationships between individual instances made explicit (e.g., users' movie ratings, social network links)?**

    Không có quan hệ tường minh giữa các instance.


8. **Are there recommended data splits (e.g., training, development/validation, testing)?**

    Tập dữ liệu được chia stratified 80/20 theo nhãn profitable với random_state=42, lưu thành movie_train.csv và movie_test.csv. Không có tập validation cố định; cross-validation được khuyến nghị khi tinh chỉnh mô hình.


9. **Are there any errors, sources of noise, or redundancies in the dataset?**

    Có, bộ dữ liệu có tồn tại một số nguồn nhiễu, sai số tiềm ẩn và giới hạn về tính đại diện, cụ thể như sau:

    - Sai số từ nguồn thu thập: Dữ liệu được trích xuất từ IMDb và TMDB API. Do tính chất của các nền tảng này là tổng hợp tự động và có sự đóng góp từ cộng đồng, thông tin không thể đảm bảo độ chính xác và tin cậy tuyệt đối.

    - Nhiễu tại ranh giới phân lớp: Việc sử dụng một ngưỡng cứng là 2.5x ngân sách để xác định nhãn có lãi (profitable) tạo ra một vùng nhiễu tại ranh giới phân chia. Phân tích cho thấy có khoảng 5.5% số lượng phim nằm trong vùng ranh giới từ 2.3x đến 2.7x, có khả năng gây khó khăn trong việc phân loại chính xác.

    - Selection Bias: Việc áp dụng ngưỡng đánh giá (numVotes >= 5000) kết hợp với việc loại bỏ các bộ phim thiếu thông tin tài chính đã khiến dữ liệu bị nghiêng về phân khúc phim thị trường (mainstream) và phim phát hành rộng rãi. Do đó, các dòng phim độc lập, nhỏ lẻ và phim không sử dụng tiếng Anh bị thiếu hụt đại diện ở mức độ tương đối.


10. **Is the dataset self-contained, or does it link to or otherwise rely on external resources?**

    Bộ dữ liệu sau xử lý là độc lập.


11. **Does the dataset contain data that might be considered confidential?**

    Không. Toàn bộ dữ liệu thu thập từ nguồn công khai (TMDB API, IMDb).


12. **Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety?**

    Không.


13. **Does the dataset relate to people?**

    Không.


## Collection Process


1. **How was the data associated with each instance acquired?**

    Dữ liệu được thu thập qua TMDB API và IMDb Non-Commercial Datasets. Dữ liệu CPI thu thập từ FRED (Federal Reserve Bank of St. Louis).


2. **What mechanisms or procedures were used to collect the data?**

    Thu thập tự động qua API calls.


3. **If the dataset is a sample from a larger set, what was the sampling strategy?**

    Lọc theo: có numVotes trên IMDb từ 5000 trở lên, có đầy đủ dữ liệu tài chính (budget và revenue), phạm vi phát hành 2015–2025. Không áp dụng random sampling - toàn bộ phim thỏa điều kiện đều được đưa vào.


4. **Who was involved in the data collection process and how were they compensated?**

    Toàn bộ quá trình thu thập và xử lý được nhóm sinh viên tự thực hiện.


5. **Over what timeframe was the data collected?**

    Dữ liệu được thu thập vào khoảng tháng 5 năm 2026. Dữ liệu phim bao phủ giai đoạn phát hành 2015-2025.


6. **Were any ethical review processes conducted?**

    Không. Dữ liệu thu thập từ nguồn công khai, không liên quan đến dữ liệu cá nhân nhạy cảm và không liên quan đến các nghiên cứu trực tiếp trên đối tượng con người, do đó không yêu cầu phải có sự phê duyệt từ hội đồng đạo đức.


7. **Does the dataset relate to people?**

    Không. Bộ dữ liệu này không liên quan đến các cá nhân.


## Preprocessing/Cleaning/Labeling


1. **Was any preprocessing/cleaning/labeling of the data done?**

    Có. Quá trình tiền xử lý bao gồm:

    - **Lọc missing tài chính**: drop các phim thiếu budget hoặc revenue.
    - **Tạo nhãn**: profitable = 1 nếu revenue/budget ≥ 2.5, ngược lại = 0.
    - **Train/Test split**: stratified 80/20, random_state=42.
    - **Drop features có vấn đề**: top_3_cast và director (temporal leakage + data inconsistency); startYear (sai lệch ngày ra mắt IMDb vs TMDB).
    - **Lọc scope**: drop phim ngoài phạm vi 2015–2025 dựa trên release_date.
    - **Feature engineering**: budget_adj (điều chỉnh lạm phát CPI về 2025); release_month và release_year (trích xuất từ release_date); primary_country (trích xuất từ origin_country).
    - **Encoding**: certification_us, original_language, primary_country, release_month, genres, keywords, production_companies.
    - **Transformation**: budget_adj và các cột frequency.
    - **Scaling**: RobustScaler cho các biến numeric liên tục; MinMaxScaler cho release_year.


2. **Was the "raw" data saved in addition to the preprocessed/cleaned/labeled data?**

    Có. Dữ liệu thô được lưu tại data/raw/. Dữ liệu đã xử lý hoàn chỉnh lưu tại data/processed/.


3. **Is the software used to preprocess/clean/label the instances available?**

    Có. Toàn bộ quá trình được thực hiện bằng Python.


4. **Any other comments?**

    Không.




## Uses


1. **Has the dataset been used for any tasks already?**

    Dataset được tạo ra và sử dụng trực tiếp cho bài toán phân loại nhị phân: dự đoán khả năng sinh lời của phim. Chưa được sử dụng ngoài phạm vi đồ án.


2. **Is there a repository that links to any or all papers or systems that use the dataset?**

    Không.


3. **What (other) tasks could the dataset be used for?**

    Dataset có thể được sử dụng để dự đoán khả năng sinh lời, dự đoán doanh thu hay các bài toán liên quan như phân tích xu hướng thị trường phim theo năm/thể loại/quốc gia.


4. **Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?**

    Có. Cần lưu ý:
    - **Selection bias**: tập dữ liệu thiên về phim Anh ngữ, có thông tin tài chính rõ ràng. Mô hình có thể kém chính xác hơn với phim độc lập, phim ngoài Hollywood.
    - **Ngưỡng nhãn**: ngưỡng 2.5x là một lựa chọn có tính chủ quan. Thay đổi ngưỡng sẽ ảnh hưởng đáng kể đến tỷ lệ nhãn và kết quả mô hình.


5. **Are there tasks for which the dataset should not be used?**

    Dataset không nên được dùng để đưa ra quyết định đầu tư thực tế vào phim do: (1) selection bias, (2) thiếu nhiều yếu tố quan trọng như chiến lược marketing, đối thủ cạnh tranh, review sớm, và (3) mô hình chỉ được validate trong phạm vi học thuật.


6. **Any other comments?**

    Không.




## Distribution


1. **Will the dataset be distributed to third parties outside of the entity on behalf of which the dataset was created?**

    Bộ dữ liệu có sẵn và có thể được truy cập. Tuy nhiên, nhóm chưa có ý định phân phối rộng rãi ra bên ngoài. Hiện tại bộ dữ liệu chỉ được lưu trữ trên kho lưu trữ của dự án trên GitHub nhằm mục đích học tập.


2. **How will the dataset be distributed?**

    Bộ dữ liệu có sẵn thông qua kho lưu trữ mã nguồn của dự án trên GitHub.


3. **When will the dataset be distributed?**

    Bộ dữ liệu đã được tải lên kho lưu trữ dự án trên GitHub từ tháng 6 như phiên bản hoàn chỉnh đầu tiên và sẽ tiếp tục duy trì tại đó.


4. **Will the dataset be distributed under a copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?**

    Dữ liệu được thu thập từ TMDB API (theo [TMDB Terms of Use](https://www.themoviedb.org/api-terms-of-use)) và IMDb (theo [IMDb Non-Commercial Licensing](https://developer.imdb.com/non-commercial-datasets/)). Bất kỳ việc phân phối nào cần tuân thủ các điều khoản này. Do đây là dự án học thuật, dữ liệu không áp dụng bất kỳ giấy phép bản quyền sở hữu trí tuệ riêng nào khác ngoài việc tuân thủ các quy định nêu trên.


5. **Have any third parties imposed IP-based or other restrictions on the data associated with the instances?**

    Có. TMDB yêu cầu ghi nhận nguồn khi sử dụng dữ liệu API. IMDb giới hạn sử dụng trong phạm vi phi thương mại. Nhóm cam kết tuân thủ các hạn chế này trong suốt quá trình thực hiện dự án.


6. **Do any export controls or other regulatory restrictions apply to the dataset or to individual instances?**

    Không, theo hiểu biết của nhóm.


7. **Any other comments?**

    Không.




## Maintenance


1. **Who is supporting/hosting/maintaining the dataset?**

    Nhóm sinh viên thực hiện đồ án.


2. **How can the owner/curator/manager of the dataset be contacted?**

    Qua email đại diện của nhóm: 24520170@gm.uit.edu.vn


3. **Is there an erratum?**

    Hiện tại không có. Nếu phát hiện lỗi, sẽ được ghi chú và cập nhật trong repository.


4. **Will the dataset be updated (e.g., to correct labeling errors, add new instances, delete instances)?**

    Không có kế hoạch cập nhật sau khi đồ án kết thúc.


5. **If the dataset relates to people, are there applicable limits on the retention of the data associated with the instances?**

    Không. Bộ dữ liệu không chứa thông tin cá nhân.


6. **Will older versions of the dataset continue to be supported/hosted/maintained?**

    Không. Các phiên bản cũ (nếu có) sẽ được quản lý thông qua lịch sử commit trên GitHub, nhưng sẽ không có sự hỗ trợ kỹ thuật riêng biệt cho từng phiên bản.


7. **If others want to extend/augment/build on/contribute to the dataset, is there a mechanism for them to do so?**

    Có. Những người quan tâm có thể thực hiện gửi Pull Request nếu muốn đóng góp cải thiện dữ liệu/mã nguồn. Các đóng góp sẽ được nhóm xem xét và phản hồi trong phạm vi khả năng của nhóm.


8. **Any other comments?**

    Không.
