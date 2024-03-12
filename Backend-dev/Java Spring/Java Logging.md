---
banner: "https://miro.medium.com/v2/resize:fit:1200/0*vyPkgeBB5JcDIQdR.png"
---
# Java Logging 
### WTF! is log 
- Quá trình ghi lại những thông tin được thông báo, lưu lại trong quá trình hoạt động của một ứng dụng ở một nơi tập trung. => Ncl để debug 
- How to log: 
	- Xem sau đấy có thể sử dụng log được hay không :v 
###### Log level 
![[Pasted image 20240310172508.png]]
###### Format log 
- Nên dễ đọc, dễ trace ra được thông tin cần tìm (thường dùng [Logstash](https://www.elastic.co/logstash))
###### Log rotate 
- Là việc cắt nhỏ log ra và lưu trữ trên nhiều file thay vì một file 
- VD: Lưu file log riêng theo từng ngày, từng tháng; chia theo loại log; cắt file theo dung lượng
### Log4j 
- Loggers: Lấy thông tin từ code 
- Appenders: Ghi thông tin log ra file, console, email, ... (Có thể config phần này để rotate file log)
- `Sl4j` - chỉ đơn giản là abstraction layer cho các logging framework khác như Log4j, Logback, ...

<b style="color: red">REMEMBER ALWAYS LOG IN CATCH BLOCK</b>
