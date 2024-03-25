# REST
### Rule 1: Naming 
- Tên của API nên được group theo từng chủ thể của hệ thống 
- Không được dùng động từ của hành động để đặt tên API (VD nhưu /getProduct)
- Thường sẽ có đánh dấu version ở đầu để giữ version cũ nhằm giúp client chưa update logic vẫn có thể chạy được với tập API cũ
### Rule 2: Request 
- Method của Request phải thể hiện đúng hành động nó sẽ làm
	- GET: Read data 
	- POST: Create data 
	- PUT: Update data
	- DELETE: Delete data
- Dữ liệu trong body thường sẽ sử dụng là JSON là format

### Rule 3: Response
- Status code cần được trả về đúng với status của response
- Khi server đã trả lỗi 400, 500, bắt buộc mọi thay đổi ở server đều phải được rollback/clean sạch sẽ nhằm tránh việc client retry, và mess up dữ liệu

### Rule 4: Idempotent 
- Idempotent: Một yêu cầu được gọi là idempotent nếu kết quả thành công hay thất bại không phụ thuộc vào số lần request được gọi 
=> Giúp request trở lên an toàn hơn, hữu ích khi việc gọi API bị gián đoạn trong quá trình chuyển tiếp
- Các request GET PUT DELETE đều phải là idempotent 

### Rule 5: Stateless 
- Các request giữa một client với server phải độc lập và không ảnh hưởng nhau 
- Các API cần tránh việc lưu trạng thái client, vì nếu lưuu trạng thái có nghĩa là request thứ 2 sẽ bị ảnh hưởng bởi việc request thứ 1 set trạng thái cho client trên server là gì 
- Lý do: Logic được nhất quán nếu có nhiều instance cùng chạy và cũng giúp server scale dễ hơn 

### Rule 6: Pagination
- Khi một request trả về một lượng lớn item, không được trả về toàn bộ item 1 lúc vì nó sẽ làm request chậm và ảnh hưởng tới trải nghiệm người dùng và performance hệ thống 
- Sử dụng pagination như một cách giải quyết vấn đề này 
- VD:/products?query=iphone&offset=75&limit=25

##### Parameters
- Chia làm 3 loại 
	- Path parameter: /products/detail/1920239
		- Được sử dụng cho GET, PUT, DELETE API, nhưng thường được dùng chung với body parameter nếu là PUT
	- URL parameter /products/search?query=iphone&sort=price
		- Chỉ nên được sử dụng cho GET API, tuy nhiên nên tránh dùng nếu có quá nhiều parameter vì sẽ làm url dài và xấu
	- Body parameter: /products với body {"name": "iphone", "branch": "Apple"}
		- Có thể được dùng cho mọi method nhưng vì nó khó hiểu hơn nên nếu dùng được các method khác thì tránh

##### Nhược điểm 
- multiple request problem: Nhiều request cho nhiều endpoint 
- overfetching và underfetching: dư thừa hoặc không đủ data cho application 
