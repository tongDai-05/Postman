# BÁO CÁO BÀI TẬP THỰC HÀNH LAB 7
## HỌC PHẦN: ĐÁNH GIÁ KIỂM ĐỊNH CHẤT LƯỢNG PHẦN MỀM
### ĐỀ TÀI: KIỂM THỬ TỰ ĐỘNG RESTful API VỚI CÔNG CỤ POSTMAN

---

## 👨‍🎓 THÔNG TIN SINH VIÊN
* **Họ và tên:** Tống Sỹ Đại
* **Mã sinh viên:** 23010037
* **Môn học:** Đánh giá kiểm định chất lượng phần mềm
* **Công cụ thực hiện:** Postman Desktop Application (v11)
* **Hệ thống API thử nghiệm:** [JSONPlaceholder](https://jsonplaceholder.typicode.com)
* **Tài liệu nộp bài:** GitHub Repository & Postman Collection

---

## 📑 MỤC LỤC
1. [Giới thiệu và Mục tiêu bài Lab](#1-giới-thiệu-và-mục-tiêu-bài-lab)
2. [Cơ sở lý thuyết về Kiểm thử API & Postman](#2-cơ-sở-lý-thuyết-về-kiểm-thử-api--postman)
3. [Cấu trúc thư mục Repository](#3-cấu-trúc-thư-mục-repository)
4. [Bảng thiết kế kịch bản kiểm thử (Test Matrix)](#4-bảng-thiết-kế-kịch-bản-kiểm-thử-test-matrix)
5. [Chi tiết thực thi kịch bản và Hình ảnh minh chứng](#5-chi-tiết-thực-thi-kịch-bản-và-hình-ảnh-minh-chứng)
   * [5.1. TC01 - Lấy danh sách toàn bộ bài viết (GET)](#51-tc01---lấy-danh-sách-toàn-bộ-bài-viết-get)
   * [5.2. TC02 - Lấy chi tiết bài viết theo ID (GET)](#52-tc02---lấy-chi-tiết-bài-viết-theo-id-get)
   * [5.3. TC03 - Tạo mới một bài viết (POST)](#53-tc03---tạo-mới-một-bài-viết-post)
   * [5.4. TC04 - Cập nhật thông tin bài viết (PUT)](#54-tc04---cập-nhật-thông-tin-bài-viết-put)
   * [5.5. TC05 - Xóa bài viết khỏi hệ thống (DELETE)](#55-tc05---xóa-bài-viết-khỏi-hệ-thống-delete)
6. [Báo cáo kiểm thử tự động với Collection Runner](#6-báo-cáo-kiểm-thử-tự-động-với-collection-runner)
7. [Hướng dẫn cài đặt và Chạy lại kịch bản (How to Reproduce)](#7-hướng-dẫn-cài-đặt-và-chạy-lại-kịch-bản-how-to-reproduce)
8. [Đánh giá kết quả & Bài học kinh nghiệm](#8-đánh-giá-kết-quả--bài-học-kinh-nghiệm)

---

## 1. GIỚI THIỆU VÀ MỤC TIÊU BÀI LAB

### 1.1. Bối cảnh
Trong quy trình phát triển và kiểm định phần mềm hiện đại, kiến trúc hướng dịch vụ (Service-Oriented Architecture) và kiến trúc Microservices ngày càng phổ biến. Kiểm thử tầng API (Application Programming Interface) đóng vai trò đặc biệt quan trọng vì nó nằm giữa tầng dữ liệu và giao diện người dùng, giúp phát hiện lỗi nghiệp vụ sớm (Shift-Left Testing) trước khi hoàn thiện giao diện người dùng (UI).

### 1.2. Mục tiêu đạt được
* **Nắm vững lý thuyết:** Hiểu bản chất giao thức HTTP, định dạng dữ liệu trao đổi JSON, các phương thức CRUD (`GET`, `POST`, `PUT`, `DELETE`) và ý nghĩa các mã trạng thái phản hồi HTTP (HTTP Status Codes).
* **Kỹ năng công cụ:** Sử dụng thành thạo **Postman** để xây dựng bộ kịch bản kiểm thử API (Collections).
* **Tự động hóa kiểm thử:** Viết script kiểm thử tự động bằng JavaScript kết hợp thư viện Chai Assertion của Postman (`pm.test`, `pm.expect`).
* **Kiểm thử hồi quy:** Vận hành tính năng **Collection Runner** để chạy kiểm thử hàng loạt và phân tích báo cáo kết quả.

---

## 2. CƠ SỞ LÝ THUYẾT VỀ KIỂM THỬ API & POSTMAN

### 2.1. Các phương thức HTTP cơ bản
* **`GET`**: Truy vấn và lấy dữ liệu từ Server. An toàn và không làm thay đổi trạng thái của hệ thống.
* **`POST`**: Gửi dữ liệu mới lên Server để tạo một tài nguyên mới (Resource). Thường đi kèm `Body` dưới định dạng JSON.
* **`PUT`**: Gửi dữ liệu để cập nhật hoặc thay thế toàn bộ thông tin của tài nguyên đã tồn tại dựa vào định danh (`ID`).
* **`DELETE`**: Yêu cầu xóa một tài nguyên cụ thể khỏi Server.

### 2.2. Các mã phản hồi HTTP (HTTP Status Codes) quan trọng
* **`200 OK`**: Yêu cầu xử lý thành công (thường dùng cho GET, PUT, DELETE).
* **`201 Created`**: Tạo mới tài nguyên thành công (thường dùng cho POST).
* **`400 Bad Request`**: Dữ liệu gửi lên không đúng định dạng.
* **`404 Not Found`**: Không tìm thấy tài nguyên theo URL yêu cầu.
* **`500 Internal Server Error`**: Lỗi xử lý từ phía máy chủ.

### 2.3. Cơ chế Postman Test Script
Postman chạy trên nền Node.js sandbox, cho phép thực thi mã JavaScript ngay sau khi nhận được Response. Chúng ta sử dụng đối tượng `pm` để kiểm tra kết quả:
* `pm.response.to.have.status(code)`: Kiểm tra mã trạng thái HTTP.
* `pm.expect(pm.response.responseTime).to.be.below(time)`: Kiểm tra thời gian phản hồi (Performance SLA).
* `pm.expect(jsonData.property).to.eql(value)`: Kiểm tra tính đúng đắn của dữ liệu trả về.

---

## 3. CẤU TRÚC THƯ MỤC REPOSITORY

Toàn bộ tài nguyên phục vụ bài Lab 7 được tổ chức chuẩn hóa trong Repository:

```text
tongDai-05/Postman/
│
├── Lab7_Postman_Collection.json   # File Collection chứa 5 kịch bản test kèm mã kiểm thử tự động
├── README.md                      # Báo cáo chi tiết toàn bộ bài thực hành Lab 7
│
├── tc01_get_all.png               # Ảnh minh chứng TC01 (GET All Posts - 3/3 Passed)
├── tc02_get_by_id.png             # Ảnh minh chứng TC02 (GET Single Post - 2/2 Passed)
├── tc03_post_create.png           # Ảnh minh chứng TC03 (POST Create Post - 2/2 Passed)
├── tc04_put_update.png            # Ảnh minh chứng TC04 (PUT Update Post - 2/2 Passed)
├── tc05_delete.png                # Ảnh minh chứng TC05 (DELETE Post - 1/1 Passed)
└── collection_runner.png          # Ảnh minh chứng kết quả chạy tự động Collection Runner
