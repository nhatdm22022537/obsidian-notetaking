---
banner: "https://miro.medium.com/v2/resize:fit:1200/0*vyPkgeBB5JcDIQdR.png"
---
# ModelMapper 
### Cách sử dụng 
- Trong Maven:
```xml 
<dependency> 
<groupId>org.modelmapper</groupId> <artifactId>modelmapper</artifactId> <version>2.3.0</version> 
</dependency>
```
- Trong Gradle:
```gradle
compile 'org.modelmapper:modelmapper:2.3.0'
```
- Sau đó ta phải tạo một object của ModelMapper trước
```java
@Configuration 
public class ModelMapperConfig {
	@Bean 
	public ModelMapper modelMapper() {
		ModelMapper modelMapper = new ModelMapper();
		modelMapper.getConfiguration().setMatchingStrategy(MatchingStrategies.STRICT);
		return modelMapper;
	}
}
```
- Lúc nào cần thì lấy bean ModelMapper ra dùng thôi
```java 
@Service 
public class UserService {
	@Autowired 
	private final ModelMapper mapper;
	public UserDto getUser(String username) {
		User user = userRepository.findByUsername(username);
		UserDto userDto = mapper.map(user, UserDto.class);
		return userDto;
	}
}
```
### Vài điều cần lưu ý
##### Các mức độ matching 
- Chiến lược map chuẩn: `MatchingStrategies.STANDARD`
- Chiến lược map lỏng lẻo: `MatchingStrategies.LOOSE`
- Chiến lược map chặt chẽ: `MatchingStrategies.STRICT`
=> Tóm lại nên dùng Standard/strict
##### Tuỳ chỉnh cấu hình map
*Quá lười để viết tay ra hết :(*
![[Pasted image 20240309005558.png]]
##### Nên dùng getter và setter 
- Do các field toàn là private, object nguồn thì getter, đích setter (chỉ vậy thôi)

##### Luôn luôn phải test 
- Khi sử dụng model mapper, nhất thiết phải kiểm tra kết quả map (Xem nó có đúng hay ko, ko đúng thì ăn đb, ăn cax)