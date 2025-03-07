---
title : "Notification"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

Ở phần Notification này, chúng ta sẽ cài đặt server **Notification** để gửi thông báo qua email kết quả của Jenkins pipeline, các file dependency check và Trivy.

- Đầu tiên, đối với email, cần đảm bảo rằng email đã được kích hoạt cài đặt bảo mật 2 lớp. Vào phần **Security** của tài khoản Google, chọn **2-Step Verification** và bật nó lên.

![ConnectPrivate](/images/anh94.png)

- Tạo app password [tại đây](https://myaccount.google.com/apppasswords?continue=https://myaccount.google.com/security?utm_source%3Dchrome-profile-chooser%26authuser%3D0&rapt=AEjHL4NgvvgGbYRp-5gBAHtRuy7YbMech6wd7Q0LtrKAsGMal6KxMurQJ7V6-7jbEtIKcCWLR9CxOKt7x8l2Krrtfh9kNWzSBGtm89EpF7L0JL-rXjgBPto) và lưu lại.

![ConnectPrivate](/images/anh95.png)

- Vào cài đặt **System** của Jenkins, cuộn xuống phần **Email Notification** và điền thông tin như bên dưới.

{{% notice note %}}
Password là app password đã tạo ở bước trước.
{{% /notice %}}

![ConnectPrivate](/images/anh96.png)

- Để test thử mail có được gửi thành công hay chưa, chọn option **Test configuration by sending test e-mail** và chọn **Test configuration**.

![ConnectPrivate](/images/anh97.png)

- Sau khi test thành công, nhấn **Apply** và **Save**. Tạo credential thông tin email và password để sử dụng trong Jenkins pipeline như dưới đây.

![ConnectPrivate](/images/anh98.png)

- Quay trở lại cài đặt **System** của Jenkins, cuộn xuống phần **Extended E-mail Notification** và điền thông tin như bên dưới.

![ConnectPrivate](/images/anh99.png)
![ConnectPrivate](/images/anh100.png)

- Sau khi điền đầy đủ thông tin, nhấn **Apply** và **Save**. Quay lại mục **Configure** của pipeline **DevSecOps** tạo ở bước trước.

![ConnectPrivate](/images/anh101.png)

- Trong **Pipeline Script**, thêm đoạn script sau để gửi email thông báo kết quả của pipeline.

```groovy
post {
        always {
            emailext attachLog: true, 
            subject: "'${currentBuild.result}'",
            body: "Project: ${env.JOB_NAME} <br/>",
            "Build Number: ${env.BUILD_NUMBER} <br/>",
            "URL: ${env.BUILD_URL} <br/>",
            to: "ngacbaohan@gmail.com",
            attachmentsPattern: 'trivyfs.txt, trivyimage.txt'
        }
    }
```

- Đoạn script được đặt như bên hình dưới.

![ConnectPrivate](/images/anh102.png)

- Nhấn **Save** để lưu lại cấu hình. Bây giờ, chạy lại pipeline **DevSecOps** và kiểm tra xem email có được gửi thành công hay không.

![ConnectPrivate](/images/anh103.png)

- Kiểm tra trong Email đã nhận được thông báo kết quả của pipeline.

![ConnectPrivate](/images/anh104.png)

Vậy là đã cài đặt xong thông báo qua email cho Jenkins pipeline.












