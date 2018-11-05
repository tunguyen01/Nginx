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

### 3. Ưu điểm nổi trội của Nginx so với Apache

Nginx được viết với một mục tiêu rõ ràng là hoạt động tốt hơn máy chủ web Apache.

Apache chờ một kết nối hoàn thiện để thực hiện một kết nối khác theo tính tuần tự. Nhưng NginX cho phép kết nối song song nhiều truy vấn cùng một lúc. Điều này có ý nghĩa vô cùng lớn với các trang bận rộn, lượng truy cập lớn.

Nginx sử dụng bộ nhớ ít hơn đáng kể so với Apache và có thể xử lý yêu cầu nhiều gấp bốn lần mỗi giây.

### 4. Nginx proxy

#### 4.1 Proxy server là gì?

Proxy server đóng vai trò làm trung gian giữa người dùng trạm và Internet.

Proxy server xác định những yêu cầu từ client và quyết định đáp ứng hay không đáp ứng, nếu yêu cầu được đáp ứng, proxy server sẽ kết nối với server thật thay cho client và tiếp tục chuyển tiếp đến những yêu cầu từ client đến server, cũng như đáp ứng những yêu cầu của server đến client. Vì vậy proxy server giống cầu nối trung gian giữa server và client.

Hiểu một cách đơn giản là : Proxy server là một trung tâm cài đặt các proxy .Mà các proxy này nằm giữa máy tính của bạn và tài nguyên internet (bộ đệm) mà bạn đang truy nhập . Dữ liệu mà bạn yêu cầu đến proxy trước , rồi sau đó nó mới truyền dữ liệu cho bạn và ngược lại.

#### 4.2 Ý nghĩa của Proxy server

Proxy không chỉ có giá trị bởi nó làm được nhiệm vụ của một bộ lọc thông tin, nó còn tạo ra được sự an toàn cho các khách hàng của nó, Firewall Proxy ngăn chặn hiệu quả sự xâm nhập của các đối tượng không mong muốn vào máy của khách hàng. Proxy lưu trữ được các thông tin mà khách hàng cần trong bộ nhớ, do đó làm giảm thời gian truy tìm làm cho việc sử dụng băng thông hiệu quả.

Proxy server giống như một vệ sĩ bảo vệ khỏi những rắc rối trên Internet. Một Proxy server thường nằm bên trong tường lửa, giữa trình duyệt web và server thật, làm chức năng tạm giữ những yêu cầu Internet của các máy khách để chúng không giao tiếp trực tiếp Internet. Người dùng sẽ không truy cập được những trang web không cho phép (bị cấm).

Mọi yêu cầu của máy khách phải qua Proxy server, nếu địa chỉ IP có trên proxy, nghĩa là website này được lưu trữ cục bộ, trang này sẽ được truy cập mà không cần phải kết nối Internet, nếu không có trên Proxy server và trang này không bị cấm, yêu cầu sẽ được chuyển đến server thật, DNS server... và ra Internet. Proxy server lưu trữ cục bộ các trang web thường truy cập nhất trong bộ đệm để giảm chi phí kết nối, giúp tốc độ duyệt web nhanh hơn.

Proxy server bảo vệ mạng nội bộ khỏi bị xác định bởi bên ngoài bằng cách mang lại cho mạng hai định danh: một cho nội bộ, một cho bên ngoài. Điều này tạo ra một "bí danh" đối với thế giới bên ngoài và gây khó khăn đối với nếu người dùng "tự tung tự tác" hay các hacker muốn xâm nhập trực tiếp máy tính nào đó.

#### 4.3 Nginx proxy

Một lý do để thực hiện proxy các server khác với Nginx là khả năng mở rộng quy mô ra cơ sở hạ tầng. Nginx được xây dựng để xử lý nhiều kết nối đồng thời cùng một lúc. Điều này làm cho nó lý tưởng cho là điểm liên lạc chung cho client. Các server có thể chuyển các yêu cầu đối với bất kỳ số lượng backend server nào đến nó để xử lý phần lớn công việc, sau đó phản hồi các truy cập từ bất cứ đâu trên cơ sở hạ tầng của bạn. Thiết kế này cũng cung cấp cho bạn sự linh hoạt và dễ dàng hơn trong việc bổ sung thêm backend server để mở rộng hệ thống cũng như gỡ nó xuống khi cần thiết để bảo trì.

Nginx thường được thiết lập như một giải pháp reverse proxy để giúp mở rộng ra cơ sở hạ tầng và chuyển các yêu cầu đến các server khác mà bản thân chúng không được thiết kế để xử lý lưu lượng truy cập trên client lớn.

Xuyên suốt bài viết, ta sẽ đề cập đến cách làm thế nào để mở rộng hệ thống bằng cách sử dụng khả năng cân bằng tải (built-in load balancing) của Nginx.

### 5. Nginx Load balancing

Load balancing hay còn gọi là cân bằng tải, là một kỹ thuật thường được sử dụng để tối ưu hóa việc sử dụng tài nguyên, băng thông, giảm độ trễ và tăng cường khả năng chịu lỗi.

Khi chúng ta có nhiều hơn một **Web Server**, cùng với đó là sự ra tăng lưu lượng truy cập thì việc bổ sung thêm một máy chủ để phân phối lưu lượng này một cách hợp lý là cần thiết. Máy chủ này được gọi là **Load balancer**.

Nginx load balancing có thể thực hiện tại các lớp mạng khác nhau. Load balancing chạy ở 2 lớp mạng là:
* Load balancing layer 4: chuyển tiếp gói tin TCP raw đến máy chủ ứng dụng
* Load balancing layer 7: phân tích các tiêu đề HTTP trước khi chuyển tiếp đến máy chủ ứng dụng

### 6. Load balancing layer 7

<img src="https://imgur.com/a/JxLKxlQ" >

#### 6.1 Một HTTP proxy đơn giản

Loại proxy cơ bản và trực tiếp nhất là chuyển tiếp yêu cầu đến một server đơn có thể liên lạc với proxy server qua giao thức HTTP được biết đến như một "proxy pass" chung được xử lý bằng một lệnh tên là ```proxy pass``` .

Khi một yêu cầu khớp với địa chỉ trong ```proxy pass``` nhất định, yêu cầu đó sẽ được điều hướng đến URL trong location context đó.

Ví dụ:

```
# server context
location /match/here {
  proxy_pass http://example.com
}
```

#### 6.2 Định nghĩa một Upstream Context để cân bằng tải cho kết nối proxy

Trong ví dụ trước, chúng tôi biết làm thế nào để thực hiện một http proxy đơn giản đến một backend server duy nhất. Nginx cho phép chúng ta dễ dàng mở rộng cấu hình này ra bằng cách xác định toàn bộ backend server mà ta có thể chuyển yêu cầu tới.

Với lệnh ```upstream``` , ta có thể định nghĩa một tập hợp các server, với giả sử tất cả các server này đều có khả năng xử lí các yêu cầu. Điều này cho phép mở rộng cơ sở hạ tầng mà không gặp quá nhiều khó khăn.

Dưới đây là một ví dụ đơn giản:

```
# http context
upstream backend_hosts {
  server host1.example.com;
  server host2.example.com;
  server host3.example.com;
}
server {
  listen80;
  server_name example.com;
  location /proxy-me {
      proxy_passhttp://backend_hosts;
      }
}
```
Trong ví dụ trên, ta đã thiết lập một upstream context là ```backend_hosts```. Khi đã được xác định, tên này sẽ có sẵn để sử dụng trong phạm vi ủy quyền đi như thể nó là một tên miền thông thường. Như bạn có thể thấy, trong server block , ta có thể chuyển bất kỳ yêu cầu nào đến ```example.com/proxy-me/...``` tới pool được chỉ ra ở trên. Trong "pool" đó, một host được chọn bằng cách áp dụng một thuật toán có thể cấu hình. Theo mặc định, đây chỉ là một quá trình lựa chọn round-robin đơn giản.

#### 6.3 Thuật toán cân bằng tải trên Upstream server

Các thuật toán cân bằng tài thường dùng:

* (**round robin**): Thuật toán mặc định được sử dụng nếu không có thuật toán khác. Mỗi server trong upstream context được truyền các yêu cầu đến một cách lần lượt.
* ```least_conn```: Chỉ định rằng các kết nối mới luôn nên được chuyển đến các backend mà có số lượng các kết nối hoạt động ít nhất để đảm bảo cân bằng. Điều này đặc biệt hữu ích trong trường hợp kết nối vào backend có thể kéo dài một thời gian.
* ```ip_hash```: Thuật toán cân bằng này phân phối yêu cầu đến các máy chủ khác nhau dựa trên địa chỉ IP của client. Ba octet đầu tiên được sử dụng như một chìa khóa để quyết định trên máy chủ để xử lý các yêu cầu. Kết quả là client có xu hướng được phục vụ bởi mỗi máy chủ một lần, có thể hỗ trợ cho việc luân phiên hệ thống.
* ```hash```: Thuật toán cân bằng này được sử dụng chủ yếu với các ủy quyền sử dụng bộ nhớ đệm. Các máy chủ được chia dựa trên giá trị của một hash key ngẫu nhiên. Hash key này có thể là văn bản, biến, hoặc kết hợp cả hai. Đây là phương pháp cân bằng duy nhất yêu cầu người dùng cung cấp dữ liệu, chính là hash key được sử dụng.

Sau khi thay đổi thuật toán, khối upstream thu được sẽ như sau:
```
# http context
upstreambackend_hosts {
  least_conn;
  server host1.example.com;
  server host2.example.com;
  server host3.example.com;
}. . .
```
Ở ví dụ trên, server sẽ được lựa chọn ưu tiên theo số lượng kết nối đang có.

Trong phần mô tả các backend server, mặc định các server sẽ có "tải trọng" như nhau, nghĩa là giả sử rằng mỗi server có thể xử lí lượng tải như nhau. Tuy nhiên bạn có thể thay đổi tải trọng của server trong phần mô tả của nó như sau:
```
# http context
upstreambackend_hosts {
  server host1.example.com weight=3;
  server host2.example.com;
  server host3.example.com;
}. . .
```
Ở ví dụ trên, host1.example.com sẽ phải nhận tải trọng gấp 3 lần 2 server còn lại. Mặc định, mỗi server có tải trọng là 1.

### 7. Load balancing layer 4

<img src="https://imgur.com/a/AgDSDf6" >
