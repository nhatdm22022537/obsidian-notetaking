---
banner: "https://miro.medium.com/v2/resize:fit:1200/0*vyPkgeBB5JcDIQdR.png"
---
# Cấu trúc dự án Java Spring 
### Cấu trúc chung của ứng dụng 
- pom.xml, build.gradle, .gitignore - để cấu hình dự án 
- Tên package chính đặt ngược với tên miền 
- Các package con - mỗi pakage con thuộc layer cụ thể như [[service]] hay [[controller]]
- Thư mục resources chứa các tài nguyên của ứng dụng như hình ảnh, static file 
### Tổ chức luồng đi theo mô hình 3 lớp 
- Chỉ cần như layer nào thì hậu tố tên của layer đó. VD: AuthController, UserService,...

| Loại package | Chức năng                                                                           |
| ------------ | ----------------------------------------------------------------------------------- |
| util         | Chứa các lớp util (xử lý linh tinh), VD: convert end date                           |
| common       | Package chứa các class định nghĩa như enum, interface, class dùng chung và đơn giản |
| exception    | Có nhiệm vụ xử lý các exception trong Spring                                        |
| component    | Chứa các bean được định nghĩa còn lại nhưng không thuộc layer nào                   |


 
