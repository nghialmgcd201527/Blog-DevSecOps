---
title : "Cài đặt SonarQube"

weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

Trong bước này, chúng ta sẽ cài đặt SonarQube trên EC2 instance đã tạo ở bước trước. Các bạn hãy chạy câu lệnh dưới đây để cài đặt SonarQube:

```bash
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```

Vậy là đã tạo xong một container SonarQube trên EC2 instance. 

![ConnectPrivate](/images/anh23.png)

{{% notice note %}}
Hãy nhớ tạo thêm một inbound rule cho phép truy cập vào port 9000 trên Security Group của EC2 instance.
{{% /notice %}}

![ConnectPrivate](/images/anh24.png)

Bây giờ, chúng ta sẽ truy cập vào SonarQube thông qua trình duyệt web. Username và password mặc định để đăng nhập vào SonarQube cả hai đều là `admin`, sau đó hãy đổi password theo ý của mình.

![ConnectPrivate](/images/anh25.png)

