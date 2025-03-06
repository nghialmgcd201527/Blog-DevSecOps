---
title : "Tạo Elastic IP cho EC2 instance"

weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

Trong bước này, chúng ta sẽ tiến hành tạo Elastic IP cho EC2 instance. Elastic IP là một địa chỉ IP tĩnh được cung cấp bởi AWS. Elastic IP có thể được gán cho một EC2 instance để giữ cho địa chỉ public IP không thay đổi khi khởi động lại EC2 instance.

1. Đầu tiên, truy cập vào [giao diện quản lý Elastic IP](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Addresses:)

![ConnectPrivate](/images/anh5.png)

2. Click **Allocate Elastic IP address** để tạo một địa chỉ Elastic IP mới.

- Trong phần **Elastic IP address settings**, chọn **Amazon's pool of IPv4 addresses** và **Network border group** là **ap-southeast-1** (Trùng với region tạo EC2 instance trước đó) rồi chọn **Allocate**.

![ConnectPrivate](/images/anh6.png)

3. Elastic IP đã được tạo thành công. Click vào **Actions** và chọn **Associate Elastic IP address** để gán Elastic IP cho EC2 instance.

![ConnectPrivate](/images/anh9.png)

4. Ở trang **Asscociate Elastic IP address**, chọn **Instance** cho **Resource type** và chọn instance vừa tạo ở bước trước sau đó chọn **Associate**.

![ConnectPrivate](/images/anh10.png)



### Tạo IAM Role

Trong bước này chúng ta sẽ tiến hành tạo IAM Role. Trong IAM Role này sẽ được gán policy **AmazonSSMManagedInstanceCore**, đây là policy cho phép máy chủ EC2 có thể giao tiếp với Session Manager.

1. Truy cập vào [giao diện quản trị dịch vụ IAM](https://console.aws.amazon.com/iamv2/)
2. Ở thanh điều hướng bên trái, click  **Roles**.  

![role](/images/2.prerequisite/038-iamrole.png)

3. Click **Create role**.  

![role1](/images/2.prerequisite/039-iamrole.png)

4. Click **AWS service** và click **EC2**. 
  + Click **Next: Permissions**.  

![role1](/images/2.prerequisite/040-iamrole.png)

5. Trong ô Search, điền **AmazonSSMManagedInstanceCore** và ấn phím Enter để tìm kiếm policy này.
  + Click chọn policy **AmazonSSMManagedInstanceCore**.
  + Click **Next: Tags.**

![createpolicy](/images/2.prerequisite/041-iamrole.png)

6. Click **Next: Review**.
7. Đặt tên cho Role là **SSM-Role** ở Role Name  
  + Click **Create Role** \.

![namerole](/images/2.prerequisite/042-iamrole.png)

Tiếp theo chúng ta sẽ thực hiện kết nối đến các máy chủ EC2 chúng ta đã tạo bằng **Session Manager**.