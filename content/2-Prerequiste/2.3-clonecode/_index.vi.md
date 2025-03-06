---
title : "Kết nối vào EC2 instance"
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---

Chúng ta sẽ tiến hành kết nối vào EC2 instance bằng phương thức SSH.

1. Đầu tiên các bạn hãy mở terminal và chuyển đến thư mục chứa file key pair đã tạo trước đó.

![ConnectPrivate](/images/anh11.png) 

2. Sử dụng lệnh sau để kết nối vào EC2 instance:

```bash
ssh -i /path/key-pair-name.pem instance-user-name@instance-public-dns-name
```

3. Cập nhật tất cả các packet trên máy chủ EC2 instance bằng lệnh sau:

```bash
sudo apt update -y
```

![ConnectPrivate](/images/anh12.png) 


4. Clone code repository của chúng ta về EC2 instance bằng lệnh sau:

```bash
git clone https://github.com/nghialmgcd201527/Workshop-DevSecOps.git
```

![ConnectPrivate](/images/anh13.png) 

5. Chuyển đến thư mục chứa code repository vừa clone về và kiểm tra xem đã có file Dockerfile chưa.

```bash
cd Workshop-DevSecOps
ls
```

![ConnectPrivate](/images/anh14.png) 

6. Để deploy ứng dụng bằng Dockerfile trên, chúng ta cần cài đặt Docker trên máy chủ EC2 instance: 

```bash
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER  # Replace with your system's username, e.g., 'ubuntu'
newgrp docker
sudo chmod 777 /var/run/docker.sock
```

7. Sau khi cài đặt xong Docker, chúng ta sẽ build Docker image từ Dockerfile:

```bash
docker build -t workshop-devsecops .
```

![ConnectPrivate](/images/anh15.png) 


8. Chạy Docker container từ Docker image vừa build.

```bash
docker run -d -p 8081:3000 workshop-devsecops:latest
```

Vậy là chúng ta đã chạy Docker image thành công.

![ConnectPrivate](/images/anh20.png)

9. Truy cập vào trình duyệt quản lý inbound rule của security group trong EC2 instance để mở port 8081

- Truy cập vào mục Security của EC2 instance

![ConnectPrivate](/images/anh17.png)

- Click vào security group của EC2 instance

![ConnectPrivate](/images/anh18.png)

- Chọn **Edit inbound rules** và thêm một rule mới cho port 8081 sau đó chọn **Save rules**

![ConnectPrivate](/images/anh19.png)

10. Truy cập vào trình duyệt và nhập địa chỉ IP public của EC2 instance kèm theo port 8081 để kiểm tra ứng dụng đã chạy thành công hay chưa.

![ConnectPrivate](/images/anh21.png)

Vậy là chúng ta đã deploy Docker thành công ở local, có thể tiến hành thực hiện deploy tự động hoá từ đây.

