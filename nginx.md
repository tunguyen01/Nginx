## Tìm hiểu về  Nginx

> Tài liệu: Viết tài liệu với Nginx

================

### Mục lục


### 1. Giới thiệu Nginx

Nginx [Engine x] là một máy chủ  HTTP và Reverse proxy, một máy chủ mail proxy, và một máy chủ TCP/UDP proxy, ban đầu được viết bởi **Igor Sysoev**. Trong một thời gian dài, nó đã được chạy trên nhiều trang web đã được tải nặng của Nga bao gồm Yandex, Mail.Ru, VK, và Rambler. Theo Netcraft, Nginx đã phục vụ hay proxied 25,28% các trang web tấp nập nhất vào tháng 2018. Dưới đây là một số trong những câu chuyện thành công: Dropbox, Netflix, WordPress.com, FastMail.FM.

Nginx là phần mềm tự do và mã nguồn mở, được phát hành theo các điều khoản của một BSD- như giấy phép. MỘT phần lớn các máy chủ web sử dụng NGINX, thường là một cân bằng tải.

Dự án Nginx tập trung vào việc phục vụ số lượng kết nối đồng thời lớn (high concurrency), hiệu suất cao và sử dụng bộ nhớ thấp. Nginx được biết đến bởi sự ổn định cao, nhiều tính năng, cấu hình đơn giản và tiết kiệm tài nguyên.

### 2. Các tính năng

Nginx có thể được triển khai để phục vụ nội dung HTTP động trên mạng bằng cách sử dụng các trình xử lý FastCGI, SCGI cho các kịch bản, các máy chủ ứng dụng WSGI hoặc các modul Phusion Passenger và nó có thể phục vụ như một bộ cân bằng tải mềm.

Nginx sử dụng một cách tiếp cận hướng sự kiện không đồng bộ, thay vì các luồng, để xử lý các yêu cầu. Kiến trúc hướng sự kiện mô-đun của Nginx có thể cung cấp hiệu suất dự đoán cao hơn dưới tải trọng cao.

Tệp cấu hình mặc định Nginx là **nginx.conf**.

#### 2.1 HTTP proxy và Web server

* Khả năng xử lý hơn 10.000 kết nối đồng thời với một dung lượng bộ nhớ thấp (~ 2,5 MB cho mỗi 10k giữ kết nối HTTP không hoạt động)
* Xử lý các tập tin tĩnh, chỉ mục tập tin và tự động lập chỉ mục
* Reverse proxy với bộ nhớ đệm
* Cân bằng tải với health check
* TLS/SSL với SNI và OCSP đóng ghim hỗ trợ, thông qua openssl.
* Hỗ trợFastCGI, SCGI, uWSGI với bộ nhớ đệm
* Tên và địa chỉ IP dựa trên máy chủ ảo
* Tương thích IPv6
* WebSockets, HTTP/1,1 nâng cấp (101 giao thức chuyển mạch
), hỗ trợ giao thức HTTP/2
* URL viết lại và chuyển hướng

#### 2.2 Mail proxy

* Hỗ trợ TLS/SSL
* Hỗ trợ STARTTLS
* SMTP, POP3, và IMAP proxy
* Xác thực bằng cách sử dụng một máy chủ HTTP bên ngoài, các tính năng khác bao gồm nâng cấp thực thi và cấu hình mà không mất kết nối khách hàng, và một mô-đun dựa trên kiến trúc với cả hai lõi và hỗ trợ module của bên thứ ba.

Sản phẩm trả phí Nginx Plus bao gồm các tính năng bổ sung như cân bằng tải nâng cao và truy cập vào một bộ mở rộng của số liệu để giám sát hiệu suất.

### 3. Ưu điểm nổi trội của NginX so với Apache

Nginx được viết với một mục tiêu rõ ràng là hoạt động tốt hơn máy chủ web Apache.

Apache chờ một kết nối hoàn thiện để thực hiện một kết nối khác theo tính tuần tự. Nhưng NginX cho phép kết nối song song nhiều truy vấn cùng một lúc. Điều này có ý nghĩa vô cùng lớn với các trang bận rộn, lượng truy cập lớn.

Nginx sử dụng bộ nhớ ít hơn đáng kể so với Apache và có thể xử lý yêu cầu nhiều gấp bốn lần mỗi giây.

### 4. Nginx proxy

#### 4.1 Proxy server là gì?

Proxy server đóng vai trò làm trung gian giữa người dùng trạm và Internet.

Proxy server xác định những yêu cầu từ client và quyết định đáp ứng hay không đáp ứng, nếu yêu cầu được đáp ứng, proxy server sẽ kết nối với server thật thay cho client và tiếp tục chuyển tiếp đến những yêu cầu từ client đến server, cũng như đáp ứng những yêu cầu của server đến client. Vì vậy proxy server giống cầu nối trung gian giữa server và client.

Hiểu một cách đơn giản là : Proxy server là một trung tâm cài đặt các proxy .Mà các proxy này nằm giữa máy tính của bạn và tài nguyên internet (bộ đệm) mà bạn đang truy nhập . Dữ liệu mà bạn yêu cầu đến proxy trước , rồi sau đó nó mới truyền dữ liệu cho bạn và ngược lại.
