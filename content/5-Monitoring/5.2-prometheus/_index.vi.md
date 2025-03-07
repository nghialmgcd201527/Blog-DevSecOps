---
title : "Cài đặt Prometheus"

weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

Connect vào server Monitoring thông qua SSH và thực hiện các bước sau:

- Cập nhật các package trên server:

```bash
sudo apt update -y
```

- Tạo một tài khoản hệ thống dành riêng cho Prometheus:

```bash
sudo useradd --system --no-create-home --shell /bin/false prometheus
```

- Tải về tệp cài đặt Prometheus phiên bản 2.47.1

```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.47.1/prometheus-2.47.1.linux-amd64.tar.gz
```

![ConnectPrivate](/images/anh60.png)

- Giải nén tệp cài đặt Prometheus:

```bash
tar -xvf prometheus-2.47.1.linux-amd64.tar.gz
```

![ConnectPrivate](/images/anh61.png)

- Di chuyển vào thư mục Prometheus:

```bash
cd prometheus-2.47.1.linux-amd64
```

- Tạo thư mục lưu trữ dữ liệu và cấu hình:

```bash
sudo mkdir -p /data /etc/prometheus
```

- Di chuyển các tệp thực thi:

```bash
sudo mv prometheus promtool /usr/local/bin/
```

![ConnectPrivate](/images/anh62.png)

- Di chuyển các tệp console:

```bash
sudo mv consoles/ console_libraries/ /etc/prometheus/
```

![ConnectPrivate](/images/anh63.png)

- Di chuyển tệp cấu hình:

```bash
sudo mv prometheus.yml /etc/prometheus/prometheus.yml
```

![ConnectPrivate](/images/anh64.png)

- Cấp quyền sở hữu cho user `prometheus` với thư mục `/data` và `/etc/prometheus`:

```bash
sudo chown -R prometheus:prometheus /etc/prometheus/ /data/
```

![ConnectPrivate](/images/anh65.png)

- Tạo tệp cấu hình Systemd cho Prometheus:

```bash
sudo vi /etc/systemd/system/prometheus.service
```

- Thêm nội dung sau vào file trên:
    + Chỉ định `User` và `Group` là `prometheus` sẽ chạy dịch vụ Prometheus.
    + `ExecStart` chỉ định đường dẫn đến tệp cấu hình Prometheus, thư mục lưu trữ dữ liệu, port lắng nghe và cổng web.
    + `web.listen-address` chỉ định cổng lắng nghe của Prometheus.
    + `web.enable-lifecycle` cho phép Prometheus sử dụng API để tương tác với các dịch vụ khác.

```bash
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=prometheus
Group=prometheus
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/data \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries \
  --web.listen-address=0.0.0.0:9090 \
  --web.enable-lifecycle

[Install]
WantedBy=multi-user.target
```

![ConnectPrivate](/images/anh66.png)

- Kích hoạt và khởi động dịch vụ Prometheus:

```bash
sudo systemctl enable prometheus
sudo systemctl start prometheus
```

- Kiểm tra trạng thái của dịch vụ Prometheus:

```bash
sudo systemctl status prometheus
```

![ConnectPrivate](/images/anh67.png)

{{% notice note %}}
Hãy nhớ tạo thêm một inbound rule cho phép truy cập vào port 9090 trên Security Group của server Monitoring.
{{% /notice %}}

![ConnectPrivate](/images/anh68.png)

- Truy cập vào trình duyệt và nhập địa chỉ IP public của server Monitoring kèm theo port 9090 để kiểm tra xem Prometheus đã chạy thành công hay chưa.

![ConnectPrivate](/images/anh69.png)



