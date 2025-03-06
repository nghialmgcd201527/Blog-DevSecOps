---
title : "Tạo EC2 instance để cài đặt Jenkins, SonarQube và Trivy"
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

Trong bước này, chúng ta sẽ tạo một EC2 instance để cài đặt Jenkins, SonarQube và Trivy.

1. Đầu tiên, truy cập vào [giao diện quản lý dịch vụ EC2 của AWS](https://console.aws.amazon.com/ec2/).

- Chọn **Launch Instance** để bắt đầu tạo một EC2 instance mới.

![ConnectPrivate](/images/anh1.png) 

2. Tại trang **Launch an instance**
- Đặt tên cho instance: **Jenkins-SonarQube-Trivy**
- Chọn **Ubuntu AMI** version 22 làm hệ điều hành cho EC2 instance.
- Chọn **t2.large** làm instance type.

![ConnectPrivate](/images/anh2.png) 

- Ở phần **Key Pair**, chọn key pair đã tạo trước đó hoặc tạo mới một key pair.
- Ở phần **Network settings**, chọn **VPC default** và **Public subnet default**. Chọn **Enable** cho **Auto-assign public IP** và thêm **inbound rule** cho phương thức SSH.

![ConnectPrivate](/images/anh3.png)

- Trong phần **Configure storage**, nhập vào giá trị **25 GiB gp2** vì chúng ta sẽ cần một lượng lớn lưu trữ để cài đặt các plugins.

![ConnectPrivate](/images/anh4.png)

- Cuối cùng chọn **Launch instance** để tạo EC2 instance.

3. Chờ giây lát để EC2 instance được tạo xong như hình dưới đây

![ConnectPrivate](/images/anh8.png)


### Nội dung
  - [Tạo VPC](2.1.1-createvpc/)
  - [Tạo Public subnet](2.1.2-createpublicsubnet/)
  - [Tạo Private subnet](2.1.3-createprivatesubnet/)
  - [Tạo security group](2.1.4-createsecgroup/)
  - [Tạo máy chủ Linux public](2.1.5-createec2linux/)
  - [Tạo máy chủ Windows private](2.1.6-createec2windows/)
