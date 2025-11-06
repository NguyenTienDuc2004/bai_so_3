# bai_so_3
lap trinh web 
# Bài tập 3   : môn Phát triển ứng dụng trên nền web
Giảng viên  : Đỗ Duy Cốp
Lớp học phần: 58KTPM
Ngày giao   : 2025-10-24 13:50
Hạn nộp     : 2025-11-05 00:00
--------------------------------------------------
Yêu cầu     : LẬP TRÌNH ỨNG DỤNG WEB trên nền linux
1. Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
 - enable wsl: cài đặt ubuntu
 - sử dụng Hyper-V: cài đặt ubuntu
 - sử dụng VMware : cài đặt ubuntu
 - sử dụng Virtual Box: cài đặt ubuntu
2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)
3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)
4. Lập trình web frontend+backend:
 SV chọn 1 trong các web sau:
 4.1 Web thương mại điện tử
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - Có tính năng liệt kê các sản phẩm bán chạy ra trang chủ
 - Có tính năng liệt kê các nhóm sản phẩm
 - Có tính năng liệt kê sản phẩm theo nhóm
 - Có tính năng tìm kiếm sản phẩm
 - Có tính năng chọn sản phẩm (đưa sản phẩm vào giỏ hàng, thay đổi số lượng sản phẩm trong giỏ, cập nhật tổng tiền)
 - Có tính năng đặt hàng, nhập thông tin giao hàng => được 1 đơn hàng.
 - Có tính năng dành cho admin: Thống kê xem có bao nhiêu đơn hàng, call để xác nhận và cập nhật thông tin đơn hàng. chuyển cho bộ phận đóng gói, gửi bưu điện, cập nhật mã COD, tình trạng giao hàng, huỷ hàng,...
 - Có tính năng dành cho admin: biểu đồ thống kê số lượng mặt hàng bán được trong từng ngày. (sử dụng grafana)
 - backend: sử dụng nodered xử lý request gửi lên từ javascript, phản hồi về json.
 4.2 Web IOT: Giám sát dữ liệu IOT.
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - hiển thị giá trị mới nhất của các thông số đang giám sát, khi click vào thì hiển thị đồ thị lịch sử quá trình thay đổi (gọi grafana iframe để hiển thị)
 - backend: Sử dụng nodered để đọc dữ liệu từ các cảm biến (có thể dùng api online để lấy dữ liệu theo giời gian thực), 
   nodered sẽ lưu dữ liệu mới nhất (dạng update) vào cơ sở dữ liệu mariadb (sử dụng phpmyadmin để tạp table và quản trị lần đầu)
   nodered sẽ lưu dữ liệu (insert) vào influxdb để lưu giá trị lịch sử, để cho grafana dùng để hiển thị biểu đồ.
5. Nginx làm web-server
 - Cấu hình nginx để chạy được website qua url http://fullname.com  (thay fullname bằng chuỗi ko dấu viết liền tên của bạn)
 - Cấu hình nginx để http://fullname.com/nodered truy cập vào nodered qua cổng 80, (dù nodered đang chạy ở port 1880)
 - Cấu hình nginx để http://fullname.com/grafana truy cập vào grafana qua cổng 80, (dù grafana đang chạy ở port 3000)

Yêu cầu sinh viên lưu code trên github
có file readme.md có hình ảnh + text: ghi lại nhật ký quá trình làm bài.

CÁCH ĐÁNH GIÁ:
1. Cài đặt được môi trường: 1đ
2. Cài đặt được các docker container với cấu hình phù hợp: 1đ
3. Web chạy được, giao diện phù hợp, chạy trên web sever nginx: 2đ
4. nodered api trả về json, test được: 2đ
5. front-end có js gọi được api nodered, nhận về json, hiển thị được kết quả từ json này. 2đ
6. Bài làm có dấu ấn, giải thích rõ ràng, hiểu vấn đề: 2đ

# 1 cài đặt môi trường
cài ubuntu

<img width="1058" height="552" alt="image" src="https://github.com/user-attachments/assets/854535ac-c391-4a5b-96a7-28615833cd52" />

Lệnh này sẽ:

Cài Windows Subsystem for Linux (WSL2)

Cài Ubuntu mới nhất từ Microsoft Store

Kích hoạt các tính năng cần thiết (Virtual Machine Platform, v.v.)

<img width="486" height="286" alt="image" src="https://github.com/user-attachments/assets/3c0b8873-4b3b-4207-b169-4bf29d735ef4" />

mở và cài xong ubuntu

<img width="1073" height="509" alt="image" src="https://github.com/user-attachments/assets/4be3952d-9e1b-444c-beab-05049f2f56d1" />

cài thành cong docker

<img width="961" height="553" alt="image" src="https://github.com/user-attachments/assets/591811b1-920c-429a-a396-fcdbe6381430" />

tạo thư mục dự án 

<img width="373" height="102" alt="image" src="https://github.com/user-attachments/assets/8384ac43-9c90-4dab-976b-59509fae53be" />

file docker-compose.yml

<img width="1485" height="752" alt="image" src="https://github.com/user-attachments/assets/498c00a4-f171-4342-8e5c-08bc04c5b85a" />

chạy file thành công 

<img width="1462" height="581" alt="image" src="https://github.com/user-attachments/assets/d3c101bd-22d6-4730-a30d-93a94ed976d0" />

<img width="1917" height="612" alt="image" src="https://github.com/user-attachments/assets/f0b7b238-cd2e-45e4-afe8-ace63617cd3a" />

chạy được localhost

<img width="1698" height="241" alt="image" src="https://github.com/user-attachments/assets/261f93ce-1397-4572-a0db-c17ae605a97a" />

# cài môi trường , docker desktop , file docker-compose.yml thàh công 

# 4 web iot 

cấu hình nodered 

tạo dữ liệu cảm biến 

<img width="1238" height="485" alt="image" src="https://github.com/user-attachments/assets/5e7e4274-cde9-4492-b96e-29e736b5aa5d" />

truy vấn dữ liệu 

<img width="1229" height="466" alt="image" src="https://github.com/user-attachments/assets/b9d46bf3-3498-4e5c-8f03-ec5dc093db3b" />

định dạng json 

<img width="623" height="381" alt="image" src="https://github.com/user-attachments/assets/46de39f0-6e09-402a-aec4-a5255ac8444d" />


kết quả truy vấn 

<img width="513" height="761" alt="image" src="https://github.com/user-attachments/assets/d02a7946-d5ac-4a81-980b-7caa867c38a4" />

# 5 nginx làm web sever
cài file host

<img width="735" height="327" alt="image" src="https://github.com/user-attachments/assets/4084ff36-1cd7-4380-a537-4de0c28f871f" />

<img width="1353" height="243" alt="image" src="https://github.com/user-attachments/assets/b6fbf747-54a7-4517-9be0-d7f683f06d8e" />

kết quả

<img width="365" height="40" alt="image" src="https://github.com/user-attachments/assets/ab12b441-9b49-47f4-8abc-7633035b469b" />

# cấu hình nginx làm web sever ok 

kết quả 

<img width="1859" height="910" alt="image" src="https://github.com/user-attachments/assets/73215fe9-9bae-46a9-a5bf-0bef4929e06e" />


<img width="1816" height="926" alt="image" src="https://github.com/user-attachments/assets/e8923142-7605-4d6e-9636-e14f5be60a26" />

# không gọi được API đăng nhập 



