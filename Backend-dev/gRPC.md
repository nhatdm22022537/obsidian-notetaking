# gRPC 

- Thay vì các API được define bằng docs và client phải dựa vào để viết request/response tương ứng thì RPC sẽ define các function (tương ứng với 1 api) sau đó sẽ có một lib giúp generate code cho cả phía server và client cùng dùng, khi client gọi một function thì function tương ứng trên server sẽ được gọi tới
- Người dùng không cần quan tâm format gói tên mà library sẽ tự động mã hoá, encode/decode tối ưu nhất 
- RPC được implement trên nền TCP 
- Các RPC lib phổ thông như apache thrift, gRPC
##### Ưu điểm 
- Gói tin được thư viện tối ưu về tốc độ encode/decode 
- Hỗ trợ nhiều use case phức tạp như streaming(data liên tục), bidirectional(gửi nhận 2 chiều) mà nếu được thực hiện trên HTTP sẽ phức tạp hơn 
##### Nhược điểm 
- Khó đọc hiểu gói tin + khó debug vì các gói tin đã được encode 
- Không flexible = HTTP vì muốn thay đổi interface ta cập nhật cả 2 bên client và server
