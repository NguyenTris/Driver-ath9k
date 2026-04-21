# Driver-ath9k
Cải tiến cơ chế quản lý truyền gói tin (TX Queue Management) trong driver ath9k

#Cách cài đặt và demo kiểm thử<br>
#Chuẩn bị môi trường<br>
sudo apt-get update<br>
sudo apt-get install build-essential linux-headers-$(uname -r)<br>
<br>
#Tải mã nguồn từ GitHub cá nhân đã được debug<br>
git clone https://github.com/NguyenTris/Driver-ath9k.git<br>
cd drivers\net\wireless\ath\ath9k<br>
<br>
#Biên dịch và cài đặt module<br>
make -C /lib/modules/$(uname -r)/build M=$(PWD) modules		#biên dịch<br>
sudo modprobe -r ath9k						#gỡ bỏ driver cũ<br>
sudo insmod ath9k.ko						#nạp driver mới đã chỉnh sửa<br>
<br>
#Kiểm tra và chạy thử nghiệm<br>
dmesg | tail -f<br>
<br>
#Kiểm tra tải mạng: Sử dụng công cụ iperf3 để tạo lưu lượng lớn và quan sát cách hàng đợi xử lý:<br>
Máy khách (Client): iperf3 -c [IP_Server] -t 60<br>
Quan sát log: Theo dõi giá trị axq_depth và sự thay đổi giữa ngắt/polling qua NAPI.<br>
