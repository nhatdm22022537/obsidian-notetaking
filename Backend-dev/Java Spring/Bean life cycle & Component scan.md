---
banner: "https://miro.medium.com/v2/resize:fit:1200/0*vyPkgeBB5JcDIQdR.png"
---
# Bean life cycle & Component scan 
### Bean life cycle
![[Pasted image 20240308173657.png]]
- Nhìn chung là gồm các bước sau:
	1. IoC container tạo bean bằng cách gọi constructor 
	2. Gọi các setter method để inject bean bằng setter based injection 
	3. @PostConstruct được gọi 
	4. Init method được gọi
- Sau đó bean sẽ sẵn sàng hoạt động, nếu nó dừng thì:
	1. Gọi @PreDestroy 
	2. Huỷ bean như các object thông thường 
### @PostConstruct & @PreDestroy
- Nhìn chung:
	- *@PostConstruct* dùng để thực hiện một số task khi khởi tạo bean 
	- *@PreDestroy* dùng để thực hiện các task dọn dẹp bean sau khi dùng xong 

<b style="color: yellow">VÍ DỤ</b>
```java 
class AnimeGirl {
	@Autowired 
	private final Clothes clothes;
	@PostConstruct 
	//Test xem waifu mặc áo có ngon lành không (mặc xong thì cởi)
	public void testWaifu(){
		clothes.wear();
		clothes.tearoff();
	}
	//Dùng xong waifu thì xé áo và trả về nơi sản xuất =))
	@PreDestroy 
	public void tearOffClothes(){
		clothe.tearoff();
	}
}
```
### Các loại bean 

|      Loại      |                      Công dụng                      |
|:--------------:|:---------------------------------------------------:|
|   Singelton    |    IoC container tạo đúng 1 object từ class này     |
|   Prototype    | Return 1 bean object riêng biệt cho mỗi lần sử dụng |
|    Request     |            Tạo mỗi bean cho mỗi request             |
|    Session     |            Tạo mỗi bean cho mỗi Session             |
| Global Session |                         ...                         |
- Singleton bean thì là mặc định 
- Muốn chỉ định bean khác thì dùng *@Scope("prototype")*
```java 
@Component 
@Scope("prototype")
class PrototypeBean {
	...
}
```
### Cách định nghĩa bean
##### Dùng XML, annotations
```xml
<?xml version = "1.0" encoding = "UTF-8"?>
<beans xmlns = "http://www.springframework.org/schema/beans"
    xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation = "http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    
    <!-- Đây là bean Car -->
    <bean id="" class="Car" init-method="testRun">
        <!-- Cấu hình thuộc tính property cho bean -->
    </bean>
</beans>
```
*Cách này khá bủh :(*
- Giờ chỉ cần *@Component* phát là oke ngay 
##### Dùng @Bean bên trong @Configuration 
- Thường dùng trong trường hợp bean cần thực hiện nhiều thao tác phức tạp để khởi tạo, nhiều bean liên quan tới nhau 
-> Gom chung các bean cần khởi tạo bỏ vào class chứa *@Configuration* 
```java 
@Configuration 
public AppConfig() {
	
}
@Bean 
public Car carBean() {
	return new Car();
}
@Bean 
public PasswordEncoder passwordEncoderBean() {
	return new BCryptPasswordEnter();
}
//Có thể định nghĩa nhiều Bean khác với @Bean
```
### Component scan
- Class đánh dấu @SpringBootApplication chứa main method sẽ là nơi bắt đầu
- Spring Bôt sẽ tìm từ package này tìm xuống để tạo các Bean 
###### Tuỳ chỉnh package tìm kiếm 
- Dùng *@ComponentScan*
```java 
@ComponentScane("com.example.demo.component")
```
- Thêm thuộc tính *@SpringBootApplication scanBasePackages*
```java 
@SpringBootApplication(scanBasePackages = {
	"com.example.demo.components",
	"com.example.demo.controllers"
})
public class DemoApplication {
	public static void main(String[] args){
	}
}
```


