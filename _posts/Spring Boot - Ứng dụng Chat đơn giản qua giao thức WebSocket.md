## Spring Boot - Ứng dụng Chat đơn giản qua giao thức WebSocket

### WebSocket

Là một giao thức trao đổi dữ liệu hai chiều giữa Client và Server, nó sử dụng giao thức TCP (Transmission Control Protocol) thay vì HTTP.

### Ưu điểm của WebSocket

Websocket cung cấp giao thức 2 chiều rất mạnh mẽ nên có độ trễ rất thấp và dễ sửa lỗi. Thông tin trả về từ websocket là vô cùng nhanh chóng nên nó được sử dụng trong nhiều trường hợp cần thời gian thực như là chat, hiển thị biểu đồ hay thông tin chứng khoán.

### So sánh giữa Websocket và HTTP

Thông thường khi sử dụng giao thức kết nối HTTP để truyền tải dữ liệu với kỹ thuật Ajax sẽ tồn tại nhược điểm là có chứa nhiều dữ liệu không cần thiết ở phần header. Đối với HTTP, 1 header dùng để request/response thường có kích thước trong khoảng 871 byte. Trong khi nếu so với Websocket sau khi kết nối thì kích thước này chỉ là 2 byte. 

### Cấu trúc Websocket

Tương tự như (http:// và https://) websocket cũng có 2 chuẩn thông thường là ws:// và chuẩn secure là wss://

### STOMP

Streaming Text Oriented Messaging Protocol - Giao thức truyễn dẫn văn bản thiên về nhắn tin, thuộc nhánh của Websocket, nó là một giao thức văn bản thuần túy, khi client và server liên lạc với nhau theo giao thức này chúng sẽ chỉ gửi cho nhau các dữ liệu dạng tin nhắn văn bản, nó cho phép client giao tiếp với bất kỳ [message broker](https://en.wikipedia.org/wiki/Message_broker) nào hỗ trợ giao thức này. 

Tại sao chúng ta cần STOMP? WebSocket chỉ là một giao thức truyền thông, nó không xác định những thứ như - Cách gửi thư chỉ cho những người dùng đã đăng ký một chủ đề cụ thể hoặc cách gửi thư đến một người dùng cụ thể. Ta cần STOMP cho các chức năng này.

| **Chức năng**          | ** Mô tả**                                                   |
| ---------------------- | ------------------------------------------------------------ |
| Connect                | Đưa ra cách thức làm sao để **client** và **server** có thể kết nối với nhau. |
| Subscribe              | Đưa ra cách thức để **client** đăng ký (subscribe) nhận tin nhắn của một chủ đề nào đó. |
| Unsubscribe            | Đưa ra cách thức để **client** hủy đăng ký (unsubscribe) nhận tin nhắn của một chủ đề nào đó. |
| Send                   | Làm sao **client** gửi nhắn gửi tới **server**.              |
| Message                | Làm sao gửi tin nhắn gửi từ **server** đến **client**.       |
| Transaction management | Quản lý giao dịch trong quá trình truyền dữ liệu (BEGIN, COMMIT, ROLLBACK,...) |

### MessageBroker

Là một chương trình trung gian, nó tiếp nhận các tin nhắn được gửi đến trước khi phân phát tới các địa chỉ cần thiết. Vì vậy ta cần nói với **Spring** bật (enable) chương trình này cho nó hoạt động.

Hình dưới đây mô tả cấu trúc của **MessageBroker**:

![](D:\MessageBroker.png)

