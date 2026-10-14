# BÀI THỰC HÀNH KIỂM THỬ HIỆU NĂNG VỚI APACHE JMETER

> **Môn học:** Kiểm thử phần mềm  
> **Công cụ:** Apache JMeter  
> **Nội dung:** Làm quen JMeter, xây dựng Test Plan, kiểm thử HTTP và phân tích kết quả.

## 1. Mục tiêu

- Tìm hiểu mục đích và cách sử dụng Apache JMeter.
- Biết tạo Test Plan, Thread Group, HTTP Request, Assertion và Listener.
- Thực hiện kiểm thử tải cơ bản với API công khai.
- Đọc các chỉ số như số mẫu (Samples), thời gian phản hồi (Average/Min/Max), Throughput và Error %.
- Lưu Test Plan, kết quả và ảnh minh họa để nộp bài.

## 2. Giới thiệu Apache JMeter

Apache JMeter là công cụ mã nguồn mở dùng để kiểm thử tải và đo hiệu năng của ứng dụng/dịch vụ. JMeter có thể gửi yêu cầu HTTP/HTTPS, kiểm tra phản hồi bằng Assertion và tổng hợp kết quả bằng Listener hoặc báo cáo HTML.

Trong bài này, JMeter được dùng để kiểm thử API demo `https://jsonplaceholder.typicode.com`. Đây là API công khai phục vụ mục đích thử nghiệm; kết quả phụ thuộc vào mạng và tình trạng dịch vụ tại thời điểm chạy, không đại diện cho hiệu năng của một hệ thống sản xuất.

## 3. Công cụ và môi trường

- Hệ điều hành: Windows / macOS / Linux.
- Java: cài phiên bản Java được hỗ trợ bởi bản JMeter đang sử dụng.
- Apache JMeter: tải từ [trang chính thức](https://jmeter.apache.org/download_jmeter.cgi).
- API thử nghiệm: [JSONPlaceholder](https://jsonplaceholder.typicode.com/).

Kiểm tra Java trong Terminal/PowerShell:

```bash
java -version
```

Giải nén JMeter, mở thư mục `bin` và chạy `jmeter.bat` trên Windows hoặc `jmeter` trên macOS/Linux.

## 4. Cấu trúc repository

```text
JMeter-Assignment/
├── README.md
├── test-plan/
│   └── api_load_test.jmx
├── screenshots/
│   └── README.md
└── results/
    └── README.md
```

- `test-plan/api_load_test.jmx`: Test Plan có thể mở trực tiếp bằng JMeter.
- `screenshots/`: lưu ảnh chụp màn hình thực tế sau khi chạy bài.
- `results/`: lưu kết quả `.jtl` hoặc báo cáo HTML nếu cần.

## 5. Kịch bản kiểm thử

### 5.1 Cấu hình tải

| Thuộc tính | Giá trị |
|---|---|
| Số người dùng ảo (Threads) | 5 |
| Ramp-up period | 5 giây |
| Loop Count | 2 |
| Tổng số lần gửi request dự kiến | 20 (5 users × 2 vòng × 2 request) |
| Giao thức | HTTPS |
| Máy chủ | `jsonplaceholder.typicode.com` |

Mỗi vòng lặp gửi 2 request:
1. `GET /posts/1` — lấy bài viết mẫu.
2. `GET /users/1` — lấy thông tin người dùng mẫu.

### 5.2 Các thành phần JMeter

- **Test Plan:** chứa toàn bộ kịch bản kiểm thử.
- **Thread Group:** cấu hình số người dùng ảo, ramp-up và số vòng lặp.
- **HTTP Request Defaults:** đặt giao thức và máy chủ mặc định.
- **HTTP Request:** mô tả từng request GET.
- **Response Assertion:** kiểm tra HTTP status code bằng `200`.
- **JSON Assertion:** kiểm tra phản hồi có trường JSON cần thiết.
- **View Results Tree:** xem chi tiết từng request và response; chỉ dùng để kiểm tra/debug với tải nhỏ.
- **Summary Report:** xem các chỉ số tổng hợp.

## 6. Cách thực hiện

1. Cài Java và tải/giải nén Apache JMeter từ website chính thức.
2. Mở JMeter bằng `bin/jmeter.bat` (Windows).
3. Chọn **File → Open**, mở `test-plan/api_load_test.jmx`.
4. Kiểm tra cây Test Plan: Thread Group, hai HTTP Request, Assertions và Listener.
5. Nhấn **Run → Start** hoặc nút Start để chạy.
6. Mở **View Results Tree**, kiểm tra từng request. Request thành công thường hiển thị màu xanh và HTTP `200`.
7. Mở **Summary Report**, ghi lại số mẫu, thời gian phản hồi và Error %.
8. Chụp ảnh màn hình theo mục 8 và lưu vào `screenshots/`.
9. Nếu cần lưu kết quả, có thể dùng chế độ dòng lệnh như phần 7.

> Lưu ý: API công khai có thể chậm, giới hạn truy cập hoặc tạm thời không phản hồi. Nếu kết quả khác dự kiến, hãy chạy lại sau ít phút và ghi nhận đúng kết quả thực tế.

## 7. Chạy kiểm thử bằng dòng lệnh (tùy chọn)

Chạy từ thư mục `apache-jmeter-<version>/bin` hoặc thay `jmeter` bằng đường dẫn đầy đủ đến JMeter:

```bash
jmeter -n -t "duong-dan-toi/test-plan/api_load_test.jmx" -l "duong-dan-toi/results/result.jtl" -e -o "duong-dan-toi/results/html-report"
```

Thư mục `html-report` phải chưa tồn tại hoặc đang rỗng. Không chạy kiểm thử tải lớn trên dịch vụ công khai; kịch bản này chỉ có tải nhỏ để học tập.

## 8. Ảnh minh họa cần bổ sung

**Bắt buộc chụp ảnh thật sau khi chạy JMeter.** Không dùng ảnh minh họa giả lập thay cho kết quả kiểm thử.

| Tên ảnh đề xuất | Nội dung cần thể hiện |
|---|---|
| `01-test-plan.png` | Cây Test Plan và cấu hình Thread Group |
| `02-view-results-tree.png` | Kết quả request và HTTP status/response |
| `03-summary-report.png` | Summary Report sau khi chạy |
| `04-html-report.png` *(tùy chọn)* | Dashboard HTML sinh từ kết quả CLI |

Sau khi chụp, lưu ảnh vào thư mục `screenshots/` và bỏ dấu `<!-- -->` ở các dòng ảnh tương ứng để chúng hiển thị trong README.

<!--
![01 - Cấu hình Test Plan](screenshots/01-test-plan.png)
![02 - View Results Tree](screenshots/02-view-results-tree.png)
![03 - Summary Report](screenshots/03-summary-report.png)
![04 - HTML Report](screenshots/04-html-report.png)
-->

## 9. Bảng ghi nhận kết quả

Điền số liệu từ lần chạy thực tế của bạn vào bảng sau; không tự điền số liệu dự đoán.

| Chỉ số | Kết quả thực tế |
|---|---|
| Samples / Tổng request | _Điền sau khi chạy_ |
| Average response time (ms) | _Điền sau khi chạy_ |
| Min response time (ms) | _Điền sau khi chạy_ |
| Max response time (ms) | _Điền sau khi chạy_ |
| Throughput | _Điền sau khi chạy_ |
| Error % | _Điền sau khi chạy_ |

### Nhận xét kết quả

Sau khi chạy, hãy nhận xét dựa trên số liệu hiển thị:

- Các request có trả về HTTP `200` hay không?
- Error % có bằng `0.00%` không? Nếu không, mở View Results Tree để tìm lỗi.
- Average và Max response time chênh lệch nhiều không?
- Throughput thể hiện số request xử lý trong một đơn vị thời gian; chỉ so sánh trong cùng điều kiện chạy.
- Kết quả của một lần chạy nhỏ không đủ để kết luận hệ thống có thể chịu tải lớn trong thực tế.

## 10. Kết luận

Qua bài thực hành, sinh viên làm quen với giao diện JMeter, biết cấu hình người dùng ảo, gửi HTTP request, đặt điều kiện kiểm tra phản hồi và đọc báo cáo tổng hợp. Để đánh giá hiệu năng đáng tin cậy hơn, cần chạy nhiều lần, kiểm soát điều kiện thử nghiệm và sử dụng hệ thống mục tiêu được phép kiểm thử.

## 11. Tài liệu tham khảo

1. [Apache JMeter — Official Website](https://jmeter.apache.org/)
2. [Apache JMeter — Getting Started](https://jmeter.apache.org/usermanual/get-started.html)
3. [Apache JMeter — User Manual](https://jmeter.apache.org/usermanual/)
4. [JSONPlaceholder — Fake Online REST API](https://jsonplaceholder.typicode.com/)
5. [Repository tham khảo do giảng viên/gợi ý cung cấp](https://github.com/quocbinh93/JMeter)

---

**Trước khi nộp:** chạy file `.jmx`, bổ sung ảnh chụp thật, điền bảng số liệu và cập nhật URL repository GitHub của bạn.
