---
banner: "https://miro.medium.com/v2/resize:fit:1200/0*vyPkgeBB5JcDIQdR.png"
---
# Entity, domain model & DTO 
### Kiến trúc dữ liệu 
- Xét về mặt tổ chức data thì sơ đồ tổ chức dữ liệu thành các lớp sẽ như sau
![[Pasted image 20240308200651.png|1000]]
- Lý do phải chia nhiều dạng data -> Tuân theo nguyên lý seperation of concern (SoC) và đảm bảo tính S trong SOLID 
- Ngoài ra chia thành nhiều dạng data cũng đem lại tính bảo mật cho dữ liệu (1 dạng data thì sẽ bị leak các dữ liệu nhạy cảm (Quizizz))
### Các dạng data
- **Public:** Để trao đổi, chia sẻ với bên ngoài qua REST API hoặc giao tiếp với các service khác trong microservice. Data lúc này ở dạng DTO 
- **Private:** Các data dùng nội bộ trong ứng dụng, bên ngoài không nên biết, data lúc này nằm ở Domain model hoặc Entity
=> Từ đây chúng ta có 3 dạng data:

| Dạng data                  | Chức năng                                                                                                                                                    |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| DTO (Data Transfer Object) | Chuyển giữa client-server hoặc giữa các service trong microservice nhằm giảm bớt lượng info không cần thiết phải chuyển đi                                   |
| Domain model               | Các đối tượng thuộc business như Client, Report, Department,... Là các class đại diện cho kết quả tính toán, các class tham số đầu vào của service tính toán |
| Entity                     | Cũng là domain model nhưng tương ứng với table trong DB, có thể map vào DB được                                                                              |
- Các dạng data có hậu tố tương ứng, trừ Entity. VD: User - entity, UserModel - domain model, UserDto, ...
### Nguyên tắc chọn data tương ứng layer:
- **Web layer:** Chỉ nên xử lý DTO 
- **Service layer:** Nhận vào DTO (từ controler gửi qua) hoặc **Domain model** (từ các service nội bộ khác) và trả về DTO cho web layer 
- **Repository layer:** Chỉ thao tác trên Entity, có thể mapping vào DB 
Các thành phần không thuộc layer nào thì dùng **Custom Repository** - Lớp này có chức năng như lớp **Service**

