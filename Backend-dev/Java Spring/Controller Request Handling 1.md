---
banner: "https://miro.medium.com/v2/resize:fit:1200/0*vyPkgeBB5JcDIQdR.png"
---
# Xử lý request trong controller 
### Controller 
- Nơi tiếp nhận request và trả về response cho client 
- Trong code thì được đánh dấu bằng `@Controller` hoặc `@RestController`
- `@Controller` có thể trả về View qua một String hoặc JSON data trong response body (nếu được chỉ định). Thích hợp cho các controller có routing, chuyển trang các kiểu.
- `@RestController` chỉ có thể trả về data trong response body. Thích hợp cho các controller cung cấp API 
- `@RestController` = `@Controller` + `@ResponseBody`
### Cách bắt các request 
- Tên HTTP method + `mapping`. VD: `@GetMapping`, `@PostMapping`, `@PutMapping`, ...
- Có thể dùng `@RequestMapping` và chỉ định thuộc tính như sau 
```java 
@RequestMapping(value = "/users", method = RequestMethod.GET)
```
- Ngoài ra, `@RequestMapping` còn có thể dùng bên trên class controller, để chỉ định endpoint gốc cho toàn bộ method bên trong nó. Ví dụ như sau
```java
@RestController
@RequestMapping("/users")
public class UserController {
	@GetMapping("/info")
}
```
### Cách nhận request data trong Controller 
- Nhìn VD phát là hiểu ngay 
- Với `GET /users?age=18&name=Dũng`, ta có 2 request param là age và name 
- Muốn lấy 2 giá trị trên ta phải dùng `@RequestParam` như sau 
```java
@RestController
public class UserController {
    ...
    @GetMapping("/users")
    public ResponseEntity<?> getAllUsers(
        @RequestParam("age") int age,
        @RequestParam("name") String name) {
        // Lúc này hai biến age và name đã có dữ liệu tương ứng
    }
}
```
- Ngoài ra còn có các thuộc tính như `defaultValue` hay `required`

##### Path variable 
- Là một phần trong đường dẫn URL, ví dụ `GET /users/123/info` thì `123` là path variable 
```java
@GetMapping("/users/{id}/info")
public ResponseEntity<?> getUserInfo(
    @PathVariable(value = "id", defaultValue = "0") int userId) {
    // id là tên path variable, tương ứng trên url {id}
}
```
##### Request body 
- Thường method PUT, POST mới có request body, ở những TH đó, ta làm như sau:
```java
@PostMapping("/login")
public ResponseEntity<?> login(@RequestBody LoginDto loginDto) {
    // Dữ liệu trong request body có thể là JSON, form-data,...
    // Tuy nhiên khi vào controller sẽ bị parse thành object hết
}
```
##### Header 
```java
@PostMapping("/login")
public ResponseEntity<?> login(@Header("Authorization") String authHeader) {
    // Biến authHeader sẽ có giá trị là giá trị của Authorization header
}
```

