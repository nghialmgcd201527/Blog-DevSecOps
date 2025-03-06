---
title : "Cài đặt Trivy"

weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---

Để cài đặt Trivy, hãy chạy câu lệnh sau trên EC2 instance:

```bash
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```

Sau khi cài đặt xong, hãy chạy câu lệnh sau để kiểm tra xem Trivy đã cài đặt thành công chưa:

```bash
trivy version
```

![ConnectPrivate](/images/anh26.png)

Bây giờ, hãy thử scan repository của chúng ta bằng Trivy bằng cách chạy câu lệnh sau trong thư mục repository:

```bash
trivy fs .
```

Kết quả sẽ hiển thị như sau:v

![ConnectPrivate](/images/anh27.png)

Tiếp theo, hãy thử scan một Docker image bằng Trivy bằng cách chạy câu lệnh sau:

```bash
trivy image <image-id>
```

Như dưới đây là kết quả scan một Docker image:

![ConnectPrivate](/images/anh28.png)



