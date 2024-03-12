---
banner: "https://miro.medium.com/v2/resize:fit:1200/0*vyPkgeBB5JcDIQdR.png"
---
# Response
### Sơ lược về HTTP Response 
- Có 3 thông tin cần quan tâm:
	1. Status code: 200, 401(Không xác thực), 403(Không đủ quyền) và 404(Không tìm thấy)
	2. Header: Tương tự request
	3. Body: Thông báo hay dữ liệu gì đó 
### Xử lý response trong Controller 
- Với REST API, dữ liệu khi trả về sẽ nằm trong response body, dạng JSON. Như ở bài trước mình có nói, nếu dùng `@RestController` thì không cần `@ResponseBody` vì nó mặc định có rồi, còn ngược lại `@Controller` thì phải chỉ định rõ dữ liệu nằm ở đâu trong response.

<b style="color: yellow">VÍ DỤ</b>
```java 
@Controller 
public class UserController {
	@GetMapping("/")
	public String homePage() {
		return "index";
	}
	@GetMapping("/info")
	@ResponseBody
	public UserInfo getUserInfo() {
		return userInfo;
	}
}
```
##### Dùng HttpServletResponse param
- Không còn được dùng (trừ các project servlet cũ)
```java
public class UserController {
    @GetMapping("/info")
    public void getUserInfo(HttpServletRequest req, HttpServletResponse res) {
        ...
        res.setHeader("abc", "123");
        res.setStatus(404);
        ...
    }
}
```
##### Dùng class ResponseEntity
- Đây là cách được khuyến nghị 

<b style="color: yellow">VÍ DỤ</b>
```java 
public class UserController {
    @GetMapping("/info")
    public ResponseEntity<User> getUserInfo(@RequestParam("username") String username) {
        // Tìm User trong database bằng username
        User user = userRepository.findByUsername(username);
        
        // Nếu không tìm thấy, trả về message lỗi 404 Not found
        if (user == null)
            return ResponseEntity.notFound();  // Tạm thời là vậy, thực tế người ta dùng AOP để bắt exception
            
        // Nếu tìm thấy return 200 OK
        return ResponseEntity.ok(user);
    }
}
```
