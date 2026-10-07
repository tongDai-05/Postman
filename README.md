# BÁO CÁO LAB 7: KIỂM THỬ API VỚI POSTMAN

## 1. Giới thiệu chung
- **Họ và tên sinh viên:** Tống Sỹ Đại
- **Mã sinh viên:** 23010037
- **Môn học:** Đánh giá kiểm định chất lượng phần mềm
- **Mục tiêu Lab 7:**
  - Nắm vững kiến thức cơ bản về API (RESTful API), các phương thức HTTP: `GET`, `POST`, `PUT`, `DELETE`.
  - Thành thạo thao tác với công cụ **Postman**: tạo Request, thiết lập Params, Headers, Body.
  - Viết Test Script tự động để kiểm tra mã trạng thái (Status Code), Response Time, nội dung dữ liệu (JSON Schema/Values).
  - Sử dụng **Collection Runner** để thực thi kiểm thử tự động toàn bộ kịch bản test.

---

## 2. Công cụ và Môi trường thực hiện
- **Công cụ kiểm thử:** Postman (v10 / v11)
- **API thử nghiệm:** [JSONPlaceholder](https://jsonplaceholder.typicode.com) (Fake REST API dành cho testing)
- **Version Control:** Git & GitHub

---

## 3. Danh sách Test Cases (Kịch bản kiểm thử)

| Mã TC | Tên kịch bản | Phương thức | URL Endpoint | Tiêu chí đánh giá (Assertions) |
|---|---|:---:|---|---|
| **TC01** | Lấy toàn bộ danh sách bài viết | `GET` | `/posts` | Status 200, Response time < 2000ms, Trả về danh sách mảng |
| **TC02** | Lấy chi tiết bài viết theo ID | `GET` | `/posts/1` | Status 200, ID = 1, có các trường `title` và `body` |
| **TC03** | Tạo bài viết mới | `POST` | `/posts` | Status 201 Created, Kiểm tra dữ liệu trả về đúng với request body |
| **TC04** | Cập nhật thông tin bài viết | `PUT` | `/posts/1` | Status 200 OK, Kiểm tra tiêu đề mới cập nhật thành công |
| **TC05** | Xóa bài viết | `DELETE` | `/posts/1` | Status 200 OK |

---

## 4. Kết quả thực hiện và Minh họa

### 4.1. TC01 - Lấy danh sách bài viết (GET)
- **Mô tả:** Gửi yêu cầu lấy toàn bộ dữ liệu bài viết và kiểm tra response.
- **Hình ảnh minh chứng:**
![TC01 GET All](images/tc01_get_all.png)

---

### 4.2. TC02 - Lấy chi tiết bài viết theo ID (GET)
- **Mô tả:** Gửi yêu cầu lấy bài viết có `id = 1`.
- **Hình ảnh minh chứng:**
![TC02 GET Single](images/tc02_get_by_id.png)

---

### 4.3. TC03 - Tạo mới bài viết (POST)
- **Mô tả:** Gửi dữ liệu JSON kèm tiêu đề và nội dung để thêm mới bài viết.
- **Hình ảnh minh chứng:**
![TC03 POST](images/tc03_post_create.png)

---

### 4.4. TC04 - Cập nhật bài viết (PUT)
- **Mô tả:** Gửi dữ liệu mới để sửa bài viết có `id = 1`.
- **Hình ảnh minh chứng:**
![TC04 PUT](images/tc04_put_update.png)

---

### 4.5. TC05 - Xóa bài viết (DELETE)
- **Mô tả:** Gửi yêu cầu xóa bài viết có `id = 1`.
- **Hình ảnh minh chứng:**
![TC05 DELETE](images/tc05_delete.png)

---

### 4.6. Chạy tự động với Collection Runner
- **Mô tả:** Chạy toàn bộ 5 Test Cases cùng lúc bằng tính năng Collection Runner.
- **Kết quả:** Tất cả các test scripts đều đạt kết quả **Passed**.
- **Hình ảnh minh chứng:**
![Collection Runner](images/collection_runner.png)

---

## 5. Kết luận
- Đã nắm vững cách thức hoạt động của RESTful API.
- Biết cách sử dụng Postman để kiểm thử API từ cơ bản đến nâng cao (viết script kiểm thử tự động với cú pháp JavaScript của Postman `pm.test`).
- Hoàn thành đầy đủ các kịch bản test CRUD và xuất file Collection (`Lab7_Postman_Collection.json`) lưu trữ trong repository.
