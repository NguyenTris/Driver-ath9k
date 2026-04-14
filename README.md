# Driver-ath9k
Cải tiến cơ chế quản lý truyền gói tin (TX Queue Management) trong driver ath9k

#Cách cài đặt và demo kiểm thử
#Chuẩn bị môi trường
sudo apt-get update
sudo apt-get install build-essential linux-headers-$(uname -r)

#Tải mã nguồn từ GitHub cá nhân đã được debug
git clone https://github.com/NguyenTris/Driver-ath9k.git
cd ath9k-debug

#Biên dịch và cài đặt module
make -C /lib/modules/$(uname -r)/build M=$(PWD) modules		#biên dịch
sudo modprobe -r ath9k						#gỡ bỏ driver cũ
sudo insmod ath9k.ko						#nạp driver mới đã chỉnh sửa

#Kiểm tra và chạy thử nghiệm
dmesg | tail -f

#Kiểm tra tải mạng: Sử dụng công cụ iperf3 để tạo lưu lượng lớn và quan sát cách hàng đợi xử lý:
Máy khách (Client): iperf3 -c [IP_Server] -t 60
Quan sát log: Theo dõi giá trị axq_depth và sự thay đổi giữa ngắt/polling qua NAPI.
