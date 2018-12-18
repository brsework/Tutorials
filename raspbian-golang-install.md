### Raspbian và golang 
##### Author: Nam (nam@brse.work) Created at: 2012/12/18

Tôi khá là thích code bằng golang, thế nên là việc tiếp theo khi cài đặt raspberry pi này là cài cho được golang để đi cà phê chém gió với anh em vẫn có thể code được.
Đầu tiên tôi thử search trên repo mặc định của raspbian xem có gì không.
```sudo apt-cache search golang```
tìm đỏ mắt mà chỉ thấy có golang 1.8 là mới nhất trên repo, thế nên lại mày mò để cài.

Vì lười nên tôi nghĩ là viết cái script để sau này nhỡ có cài lại raspbian cũng có thể xài lại 
nên viết cái script đặt tên là `go1.11-installer.sh` . Nội dung thì đơn giản như dưới, tải cục đã build sẵn về, giải nén rồi copy vô /usr/local 
sau đó sửa lại bashrc để add thêm path đến go. 
```sh
wget https://storage.googleapis.com/golang/go1.11.1.linux-armv6l.tar.gz
sudo tar -C /usr/local -xvf go1.11.1.linux-armv6l.tar.gz
cat >> ~/.bashrc << 'EOF'
export GOPATH=$HOME/go
export PATH=/usr/local/go/bin:$PATH:$GOPATH/bin
EOF
```

Sau đó tôi chạy file script trên 
```sh
sudo chmod +x go1.11-installer.sh
sudo ./go1.11-installer.sh 
```

sau khi chạy xong để thử lại thì tôi gõ lệnh 
```
go version
```
Màn hình hiện lên dòng chữ thân thuộc `go version go1.11.1 linux/arm`, mừng quá, thành công rồi.
