# Bài thực hành kiểm thử hiệu năng với Apache JMeter

**Môn học:** Kiểm thử phần mềm  
**Công cụ:** Apache JMeter 5.6.3  
**API thử nghiệm:** JSONPlaceholder  
**Repository:** https://github.com/tuanbao205/JMeter-Assignment

## 1. Mục tiêu

- Tìm hiểu công cụ kiểm thử hiệu năng Apache JMeter.
- Biết cách xây dựng Test Plan và cấu hình Thread Group.
- Thực hiện kiểm thử HTTP Request và kiểm tra phản hồi bằng Assertion.
- Đọc các chỉ số Samples, Average, Min, Max, Throughput và Error %.
- Lưu kết quả kiểm thử và ảnh minh chứng vào GitHub.

## 2. Môi trường kiểm thử

- Apache JMeter phiên bản 5.6.3.
- Java tương thích với phiên bản JMeter sử dụng.
- Máy chủ thử nghiệm: `jsonplaceholder.typicode.com`.
- Endpoint 1: `GET /posts/1`.
- Endpoint 2: `GET /users/1`.

JSONPlaceholder là API công khai dùng cho mục đích thử nghiệm. Kết quả có thể thay đổi tùy thời điểm chạy và điều kiện mạng.

## 3. Cấu hình kịch bản kiểm thử

| Thuộc tính | Giá trị |
|---|---|
| Number of Threads | 5 |
| Ramp-up Period | 5 giây |
| Loop Count | 2 |
| Số request mỗi vòng lặp | 2 |
| Tổng số request dự kiến | 20 |
| Giao thức | HTTPS |

Tổng số request dự kiến = 5 người dùng × 2 vòng lặp × 2 request = **20 samples**.

Các thành phần chính:

- **Thread Group:** cấu hình người dùng ảo và số vòng lặp.
- **HTTP Request Defaults:** khai báo giao thức và máy chủ.
- **HTTP Request:** gửi yêu cầu GET đến hai endpoint.
- **Response Assertion:** kiểm tra mã phản hồi HTTP 200.
- **JSR223 Assertion:** kiểm tra nội dung JSON theo điều kiện đã cấu hình.
- **View Results Tree:** xem chi tiết request và response.
- **Summary Report:** tổng hợp các chỉ số hiệu năng.

## 4. Quy trình thực hiện

1. Mở Apache JMeter.
2. Chọn File → Open và mở `test-plan/api_load_test.jmx`.
3. Kiểm tra cấu hình Thread Group và hai HTTP Request.
4. Kiểm tra Assertion và các Listener được bật.
5. Nhấn Start để chạy kiểm thử.
6. Mở View Results Tree để xem mã phản hồi và nội dung JSON.
7. Mở Summary Report để ghi nhận các chỉ số.
8. Chụp ảnh minh chứng và lưu vào thư mục `screenshots/`.
9. Nếu cần, xuất kết quả JTL và báo cáo HTML vào thư mục `results/`.

## 5. Ảnh minh chứng

### 5.1 Cấu hình Test Plan

![Cấu hình Test Plan](screenshots/01-test-plan.png)

### 5.2 Kết quả request

![View Results Tree](screenshots/02-view-results-tree.png)

### 5.3 Báo cáo tổng hợp

![Summary Report](screenshots/03-summary-report.png)

### 5.4 Báo cáo HTML (nếu có)

![JMeter HTML Dashboard](screenshots/04-html-report.png)

*Lưu ý: Các ảnh cần được chụp từ lần chạy thực tế và tải lên thư mục `screenshots/` trước khi đưa vào báo cáo.*

## 6. Kết quả kiểm thử

Điền các số liệu dưới đây theo kết quả thực tế của lần chạy JMeter.

| Chỉ số | Kết quả |
|---|---|
| Tổng Samples | Điền số liệu thực tế |
| Average response time (ms) | Điền số liệu thực tế |
| Min response time (ms) | Điền số liệu thực tế |
| Max response time (ms) | Điền số liệu thực tế |
| Throughput | Điền số liệu và đơn vị |
| Error % | Điền số liệu thực tế |
| HTTP Response / Assertion | Ghi nhận kết quả thực tế |

### Nhận xét

Dựa trên kết quả kiểm thử, đánh giá số lượng request được thực thi, tỷ lệ lỗi, thời gian phản hồi trung bình và tốc độ xử lý request.

- Nếu có lỗi, kiểm tra View Results Tree để xác định nguyên nhân.
- Đối chiếu HTTP response code và trạng thái Assertion.
- So sánh Average với Min và Max để đánh giá mức biến động thời gian phản hồi.
- Chỉ đưa ra kết luận dựa trên số liệu thực tế; không sử dụng số liệu giả định.

## 7. Kết luận

Qua bài thực hành, sinh viên làm quen với Apache JMeter, biết xây dựng kịch bản kiểm thử, mô phỏng người dùng ảo, gửi HTTP Request, kiểm tra phản hồi và đọc báo cáo tổng hợp.

Kết quả thu được phản ánh điều kiện của lần chạy thử nghiệm, không đủ để khẳng định khả năng chịu tải của một hệ thống trong môi trường sản xuất. Để đánh giá chính xác hơn, cần thực hiện nhiều lần kiểm thử và ghi nhận đầy đủ môi trường thử nghiệm.

## 8. Tài liệu tham khảo

1. Apache JMeter: https://jmeter.apache.org/
2. JMeter Getting Started: https://jmeter.apache.org/usermanual/get-started.html
3. JMeter Dashboard Report: https://jmeter.apache.org/usermanual/generating-dashboard.html
4. JSONPlaceholder: https://jsonplaceholder.typicode.com/
5. Repository bài thực hành: https://github.com/tuanbao205/JMeter-Assignment

## 9. Checklist trước khi nộp

- [ ] Đã chạy Test Plan.
- [ ] Đã chụp ít nhất 3 ảnh minh chứng thực tế.
- [ ] Đã tải ảnh lên thư mục `screenshots/`.
- [ ] Đã cập nhật bảng kết quả theo số liệu thực tế.
- [ ] Đã viết nhận xét và kết luận dựa trên kết quả.
- [ ] Đã kiểm tra README hiển thị đúng trên GitHub.
