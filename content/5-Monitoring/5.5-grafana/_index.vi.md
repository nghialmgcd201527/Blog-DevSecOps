---
title : "Cài đặt Grafana"

weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

Đầu tiên, cài đặt các dependencies cần thiết:

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https software-properties-common
```

- Tải khoá GPG của Grafana và thêm vào danh sách các khoá tin cậy trên hệ thống.

```bash
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
```

![ConnectPrivate](/images/anh77.png)

- Thêm repository của Grafana vào hệ thống APT, giúp cài đặt hoặc cặt nhật Grafana qua APT.

```bash
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

- Cập nhật và cài đặt Grafana

```bash
sudo apt-get update
sudo apt-get -y install grafana
```

- Kích hoạt và khởi động dịch vụ Grafana

```bash
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

- Kiểm tra trạng thái của dịch vụ Grafana

```bash
sudo systemctl status grafana-server
```

![ConnectPrivate](/images/anh78.png)

- Truy cập vào Grafana qua địa chỉ IP của máy chủ với port 3000 (mặc định) và đăng nhập với tài khoản mặc định là `admin` và mật khẩu mặc định là `admin`.

{{% notice note %}}
Hãy nhớ tạo thêm một inbound rule cho phép truy cập vào port 3000 trên Security Group của server Monitoring.
{{% /notice %}}

![ConnectPrivate](/images/anh79.png)








