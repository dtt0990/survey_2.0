# THT Customer Feedback & Improvement Management 1.0
Phiên bản kỹ thuật: `2026-10-17-workflow-v8`

## 1. Tình trạng triển khai

**Đã cập nhật trực tiếp Google Sheet Master gốc**, không tạo nguồn dữ liệu thay thế:
https://docs.google.com/spreadsheets/d/1NVbvqA1ldmIvKOS8p9c-3y_y0B-dahfH4pg9zTjHGSs/edit

Các tab mới:

* `Insight_Rules`: 23 quy tắc tình huống nghiệp vụ dệt may, có các cụm từ VI/EN, điều kiện ngữ cảnh, nội dung phân tích và gợi ý bộ phận.
* `Combined_Rules`: 7 quy tắc kết hợp các tiêu chí.
* `Management_Rules`: 12 quy tắc cấp quản lý.
* `Insight_Results`: lưu trạng thái xem xét và mối liên hệ đến Issue chính thức.
* `Issue_Assignments`: mỗi Issue một bộ phận nhận nhiệm vụ, thời hạn và xác nhận gửi email.
* `Department_Responses`: lưu giải trình theo phiên bản, không ghi đè nội dung đã gửi.
* `Issue_Evidence`: siêu dữ liệu bằng chứng đính kèm.
* `Issue_Progress`: tiến độ khắc phục.
* `Activity_Log`: nhật ký thao tác.

Các tab lịch sử `Legacy_2026_R1`, `Legacy_Feedback_2026_R1` và các bảng khảo sát cũ được giữ nguyên. Không quy đổi số điểm 2026 lần 1 sang cách đo mới.

**Chưa triển khai Apps Script v8 hoặc cập nhật GitHub Pages lên website thật.** Cần hoàn thành hai bước cài đặt sau. Không thay `index.html` trên website trước khi API v8 đã hoạt động.

## 2. Cập nhật Apps Script

1. Mở Apps Script project đang phục vụ API `/exec` hiện tại.
2. Sao lưu toàn bộ mã đang chạy. Gói này đã có bản `rollback/Code_v7.gs` để đối chiếu.
3. Thay toàn bộ file `Code.gs` hiện tại bằng `Code.gs` trong gói.
4. Nhấn dấu **+** cạnh Files, chọn **Script**, đặt tên `Workflow`, dán toàn bộ nội dung `Workflow.gs`.
5. Lưu project, kiểm tra lệnh Build/Run nếu cần cấp các quyền Drive và Spreadsheet.
6. Chọn **Deploy > Manage deployments > Edit > New version > Deploy**. Giữ nguyên deployment URL cũ.
7. Mở URL `/exec?action=apiInfo`, kiểm tra trường `version` bằng `2026-10-17-workflow-v8`.
8. Mở `/exec?action=getSurveyConfig` và kiểm tra đầy đủ 7 câu hỏi, thang Likert, 35 diễn giải, Overall riêng.

Lưu ý: Apps Script cần được cấp quyền ghi Google Sheet và tạo thư mục Google Drive riêng khi người dùng bắt đầu tải bằng chứng. Cấp các quyền theo nguyên tắc tối thiểu. Thư mục bằng chứng được tạo ở Drive của tài khoản thực thi Apps Script, không tạo bên trong thư mục hình ảnh dùng cho website.

## 3. Cập nhật GitHub Pages

1. Mở repository GitHub `dtt0990/survey_2.0`.
2. Nên tạo branch dự phòng trước khi cập nhật production.
3. Thay duy nhất `index.html` bằng phiên bản trong gói, sau khi API đã deploy v8.
4. Giữ nguyên `assets/logo.jpg`, `assets/hero.jpg` và cấu hình DNS `survey.thttextile.vn`.
5. Mở trình duyệt ở chế độ Private/Incognito để thử nghiệm, tránh cache giao diện cũ.

## 4. Các bước kiểm tra sau triển khai

* Giao diện đầu: khách hàng thấy nút Bắt đầu khảo sát là chính; có nút Admin nhỏ ở góc trên.
* Nhấn Admin: hiển thị xác nhận nhân viên nội bộ. Nhấn Không thì quay về trang khách hàng.
* Super Admin: đăng nhập `8888`, nhìn thấy Smart Insights, Management Insights, Issues & Actions, Rule Library, nhật ký và Dashboard khảo sát.
* Bộ phận: chọn đúng một trong sáu bộ phận, xác nhận và đăng nhập bằng `6666`.
* Chọn bộ phận QA/QC không được xem hay sửa chi tiết Issue giao cho Sales, chỉ được xem số liệu khảo sát toàn công ty ở mức tổng hợp.
* Các mức khảo sát 1, 2, 3 phải có ghi chú hoặc chọn Sẽ trao đổi trực tiếp / Chưa xác minh.
* Smart Insights phát hiện hai tình huống cụ thể trong phản hồi nếu có ngữ cảnh đủ rõ. Không nhận diện lỗi từ câu phủ định.
* Super Admin duyệt/gộp/tách Issue Candidate trước khi tạo Issue chính thức.
* Super Admin giao đúng một bộ phận, đặt hạn giải trình; nhấn mở email thì ứng dụng email mặc định được gọi với người nhận bỏ trống để kiểm tra thủ công, tiêu đề có mã và thời hạn, nội dung có URL và mật khẩu 6666.
* Hệ thống **không tự ghi đã gửi** khi chỉ mở email. Chỉ thay đổi trạng thái khi Super Admin nhấn Xác nhận đã gửi.
* Bộ phận nhập tên người cập nhật, nguyên nhân, hồ sơ kiểm tra, biện pháp khắc phục và hạn đề xuất rồi trình duyệt.
* Super Admin duyệt hoặc yêu cầu bổ sung. Khi bổ sung, tạo một bản giải trình mới; bản trước vẫn lưu.
* Bộ phận cập nhật tiến độ và nộp xác minh; chỉ Super Admin đóng Issue.
* Tệp PNG, JPG, WEBP hoặc PDF có dung lượng không quá 2MB được tải lên Drive riêng; phần cập nhật cũ không bị ghi đè.
* Management Insights: nhấn số khách hàng hoặc số phản hồi sẽ mở danh sách dữ liệu làm căn cứ. Trường hợp 2 phản hồi cùng công ty chỉ tính 1 khách hàng.
* Trong Dashboard khảo sát, chuyển Overall giữa Legacy và CSAT, xuất PDF A4 ngang. PDF các kỳ mới có thêm phần Management Insights khi Super Admin đang có dữ liệu workflow; dữ liệu lịch sử 2026 R1 giữ nguyên.
* Kiểm tra các Issue quá hạn: có cảnh báo trên Dashboard, không tự gửi thư nhắc hạn.

## 5. Giới hạn và lưu ý

1. Bộ quy tắc Smart Insights là phân tích dựa trên luật, không phải AI sử dụng chatbot hoặc API AI. Nhận định nghiệp vụ chỉ là giả thuyết cần xác minh.
2. Mật khẩu `8888` và `6666` ngắn, và `6666` được gửi trong email theo yêu cầu nội bộ. Người biết mật khẩu chung có thể chọn bộ phận khác. Việc chọn tên bộ phận không thể xác minh nhân thân. Cần Super Admin kiểm tra thủ công nếu có nghi vấn. Phiên đăng nhập có hiệu lực tối đa 8 giờ. Không dùng hệ thống như kho chứa tài liệu tối mật.
3. Chỉ cập nhật Rule Library không tự sửa kết luận nguyên nhân hay hồ sơ giải trình đã có.
4. `mailto:` phụ thuộc thiết lập ứng dụng email mặc định của máy. Trình duyệt có thể yêu cầu xác nhận mở Outlook/Foxmail; nếu chưa thiết lập, người dùng cần cấu hình trên máy. Không có thông tin nào chứng minh email thực sự đã được gửi ngoài thao tác xác nhận của Admin.
5. Bộ lọc và cập nhật dữ liệu diễn ra trong Apps Script, sử dụng Google Sheet làm kho dữ liệu. Khi số lượng phản hồi tăng lớn, cần đánh giá hiệu năng và cân nhắc lưu cache hoặc chuyển sang DB chuyên dụng.
6. Đã kiểm tra cú pháp JavaScript và bộ kiểm thử logic cục bộ. Chưa chạy luồng end-to-end trên Apps Script deployment thật. Trình duyệt thử nghiệm tự động trong môi trường này bị chặn truy cập nội bộ, nên cần thực hiện checklist giao diện trên website sau khi deploy.
7. Google Sheet có bốn mã phản hồi thử cũ với 28 dòng chi tiết không tìm thấy bản ghi cha. Giữ nguyên để truy vết; không đưa vào mẫu số của dữ liệu hợp lệ.
8. Kỳ 2026_R2 đang đặt Active để thử nghiệm nhưng ngày dự kiến trong Master bắt đầu tháng 12/2026. Kiểm tra lại lịch triển khai thực tế trước khi phát hành khảo sát.

## 6. Danh sách file

* `Code.gs`: API gốc của khảo sát, Legacy/CSAT và quyền truy cập API v8.
* `Workflow.gs`: xác thực 8 giờ, Smart Insights, phân công, duyệt, ghi nhận, tài liệu, nhật ký.
* `index.html`: giao diện khách hàng và quản trị dùng chung một trang.
* `test_logic.js`: kiểm tra các thuật toán nhận diện, loại trừ phủ định, phân quyền và chỉ số tổng hợp.
* `rollback/`: hai file tham chiếu phiên bản v7 để phục hồi khi cần.

Nếu bất kỳ bước triển khai production nào thất bại, dừng ở bước đó và giữ nguyên Google Sheet Master. Không chạy lại bộ nhập dữ liệu lịch sử hoặc xóa các tab cũ.
