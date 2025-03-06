---
title : "Cài đặt và cấu hình plugin Docker"

weight : 9
chapter : false
pre : " <b> 4.9 </b> "
---

Truy cập giao diện cài đặt plugin của Jenkins như đã hướng dẫn ở bước trước, tìm kiếm plugin `Docker` và cài đặt các plugins sau.

![ConnectPrivate](/images/anh48.png)

Để có thể push Docker image lên Docker Hub, cần cấu hình thông tin credential của Docker Hub. Thực hiện tạo mới credential như bước trước.

![ConnectPrivate](/images/anh49.png)

Vào cấu hình **Tools** của Jenkins, chọn **Add Docker**. Đặt tên là `docker`, chọn **Install automatically** -> **Add Installer** -> **Download from docker.com**. Nhấn **Apply** và **Save** để lưu cấu hình.

![ConnectPrivate](/images/anh50.png)









