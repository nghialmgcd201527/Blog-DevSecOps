---
title : "Tạo EC2 instance để cài đặt Jenkins, SonarQube và Trivy"
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

Trong bước này, chúng ta sẽ tạo một EC2 instance để cài đặt Jenkins, SonarQube và Trivy.

1. Đầu tiên, truy cập vào [giao diện quản lý dịch vụ EC2 của AWS](https://console.aws.amazon.com/ec2/).

- Chọn **Launch Instance** để bắt đầu tạo một EC2 instance mới.

<!-- ảnh -->

2. Tại trang **Launch an instance**
- Đặt tên cho instance: **Jenkins-SonarQube-Trivy**
- Chọn **Ubuntu AMI** làm hệ điều hành cho EC2 instance.
- Chọn **t2.large** làm instance type.





Để tìm hiểu cách tạo các EC2 instance và VPC với public/private subnet các bạn có thể tham khảo bài lab :
  - [Giới thiệu về Amazon EC2](https://000004.awsstudygroup.com/vi/)
  - [Làm việc với Amazon VPC](https://000003.awsstudygroup.com/vi/) 


### Nội dung
  - [Tạo VPC](2.1.1-createvpc/)
  - [Tạo Public subnet](2.1.2-createpublicsubnet/)
  - [Tạo Private subnet](2.1.3-createprivatesubnet/)
  - [Tạo security group](2.1.4-createsecgroup/)
  - [Tạo máy chủ Linux public](2.1.5-createec2linux/)
  - [Tạo máy chủ Windows private](2.1.6-createec2windows/)
