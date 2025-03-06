---
title : "Cài đặt Jenkins"

weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

Chạy các câu lệnh sau để cài đặt Jenkins:

```bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)

#jenkins
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Sau khi cài đặt xong, hãy kiểm tra trạng thái của Jenkins bằng câu lệnh sau:

```bash
sudo systemctl status jenkins
```

Vậy là Jenkins đã được khởi chạy thành công.

![ConnectPrivate](/images/anh29.png)

{{% notice note %}}
Hãy nhớ tạo thêm một inbound rule cho phép truy cập vào port 8080 trên Security Group của EC2 instance.
{{% /notice %}}

![ConnectPrivate](/images/anh30.png)

Bây giờ, chúng ta sẽ truy cập vào Jenkins thông qua trình duyệt web với port 8080 và làm theo các bước hướng dẫn của Jenkins để lấy mật khẩu và cài đặt các plugin được yêu cầu.

![ConnectPrivate](/images/anh31.png)

Sau đó tạo một user mới và đăng nhập vào Jenkins.

![ConnectPrivate](/images/anh32.png)
