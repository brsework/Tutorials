#### Raspbian va apache2
Tôi đang thử triển khai một ứng dụng nodejs trên raspbian, sau khi cài đặt apache2 để có thể thiết lập virtualhost thì tôi bắt đầu suy nghĩ về việc thiết lập sao cho apache hiểu được tôi sẽ dùng cổng 3000 cho ứng dụng node.
Tôi đã thử khởi động ứng dụng của mình bằng câu lệnh `node index.js` và truy cập từ bên ngoài bằng IP của máy đang chạy thì thấy nó tự động hiển thị trang mặc định của apache2.
Sau một hồi tìm hiểu thì mới biết để trỏ config về 127.0.0.1:3000 thì trong 000-default.conf file phải thiết lập mod proxy.
Ở mặc định thì apache2 không thiết lập sẵn vì thế tôi phải tự động bật lên bằng tay thông qua 2 command bên dưới
``` sh
sudo a2enmod proxy 
sudo a2enmod proxy_http 
```
Sau khi bật xong thì chúng ta cần restart apache2
``` sh
systemctl restart apache2.services
```
Sau đó chúng ta quay lại sửa  /etc/apache2/sites-available/000-default.conf 
``` sh
sudo nano /etc/apache2/sites-available/000-default.conf 
```
Tôi thêm vào nội dung của file 
``` sh
<VirtualHost *:80>
...
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:3000/
    ProxyPassReverse / http://127.0.0.1:3000/
...
</VirtualHost>
```
Sau đó lại restart apache2 lại lần nữa
```sh
systemctl restart apache2.services
```
Quay lại thư mục node và chạy lệnh để start server của bạn lên. 
