---
banner: "https://miro.medium.com/v2/resize:fit:1200/0*vyPkgeBB5JcDIQdR.png"
---
# Bean & Application context
### Application Context 
- Là khái niệm để chỉ Spring IOC container (Nâng cao hơn BeanFactory)
- Khi Spring chạy, Spring IOC container quét tất cả các packages và đưa các bean vào ApplicationContext (Component Scan)
- Biến context ở đâu 
```java 
@SpringBootApplication
public class Application {
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
} 
```
```java
//Chúng ta có thể lấy bean từ đây khi sử dụng method getBean()
ApplicationContext context = SpringApplication.run(Application.class, args);
Car car = context.getBean(Car.class);
//Chúng ta thậm chí có thể getBean từ interface
Engine engine = context.getBean("ChinaEngine", Engine.class);
```
### Một số kỹ thuật inject 
##### Sử dụng @Autowired
```java 
@Component 
public class Car {
	@Autowired 
	private final Engine engine;
}
```
*Cách này không được khuyến nghị lắm vì đặt thẳng @Autowired trên field*

##### Inject qua constructor hoặc setter 
```java 
public class Car {
	private final Engine engine;
	public class Car(Engine engine){
		this.engine = engine;
	}
}
```
*Không cần annotation @Autowired trong các bản Spring mới*
```java 
public class Car {
	private final Engine engine;
	@Required
	public void setEngine(Engine engine){
		this.engine = engine;
	}
}
```
*Sử dụng @Required để bắt buộc*

### Xử lý trường hợp Spring không biết chọn bean nào 
- Khi này ta đơn giản dùng từ khoá @Primary hoặc @Qualified - để chỉ định rõ tên bean được inject
```java
@Component 
@Primary
public class VNEngine implements Engine{
...
}
```
```java 
@Component 
public class Car {
	@Autowired 
	@Qualified("VNEngine")
	private final Engine engine;
}
```