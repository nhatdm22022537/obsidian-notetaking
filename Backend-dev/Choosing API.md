# Choosing API
### Các yếu tốc cân nhắc 
- Data format: REST, GraphQL dùng JSON; gRPC sử dụng binary format 
- Data fetch: GraphQL 
- Browser support: REST và GraphQL còn gRPC thì có thể sử dụng extension của gRPC cho web 
- Response time: gRPC bởi HTTP2 và binary format 
- Caching: REST hỗ trợ caching ở tầng HTTP còn GraphQL sử dụng POST nên khó cache hơn

### Mix and match
![[Pasted image 20240324070636.png]]