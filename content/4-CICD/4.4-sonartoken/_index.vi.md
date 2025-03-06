---
title : "Tạo SonarQube Token"

weight : 4
chapter : false
pre : " <b> 4.4 </b> "
---

Quay lại giao diện chính của SonarQube, chọn **Administration** -> **Security** -> **Users**.

![ConnectPrivate](/images/anh36.png)

Chọn **Token** -> nhập tên cho token là **jenkins** -> **Generate**.

![ConnectPrivate](/images/anh37.png)

Copy token vừa được tạo, truy cập lại giao diện của Jenkins, chọn **Manage Jenkins** -> **Credentials**.

![ConnectPrivate](/images/anh38.png)

Chọn **System** -> **Global credentials** -> **Add Credentials**.

![ConnectPrivate](/images/anh39.png)

Chọn loại **Secret text** -> dán token của SonarQube vừa copy ở bước trước -> nhập ID là `Sonar-token` -> **Create**.

![ConnectPrivate](/images/anh40.png)






