---
title : "Cài đặt Node Exporter"

weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

Connect vào server Monitoring thông qua SSH và thực hiện các bước sau:

- Tạo một tài khoản hệ thống dành riêng cho Prometheus:

```bash
sudo useradd --system --no-create-home --shell /bin/false node_exporter
```

- Tải về tệp cài đặt Node Exporter phiên bản 1.6.1:

```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
```

- Giải nén tệp cài đặt Prometheus:

```bash
tar -xvf node_exporter-1.6.1.linux-amd64.tar.gz
```

![ConnectPrivate](/images/anh70.png)

- Di chuyển file `node_exporter` vào thư mục `/usr/local/bin/` và dọn dẹp các tệp và thư mục không còn cần thiết sau khi di chuyển:

```bash
sudo mv node_exporter-1.6.1.linux-amd64/node_exporter /usr/local/bin/
rm -rf node_exporter*
```

- Tạo tệp cấu hình Systemd cho Node Exporter:

```bash
sudo vi /etc/systemd/system/node_exporter.service
```

- Thêm nội dung sau vào file trên:
    + Chỉ định `User` và `Group` là `prometheus` sẽ chạy dịch vụ Prometheus.
    + `ExecStart` chỉ định đường dẫn đến tệp cấu hình Node Exporter, thư mục lưu trữ dữ liệu, port lắng nghe và cổng web.

```bash
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=node_exporter
Group=node_exporter
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/node_exporter --collector.logind

[Install]
WantedBy=multi-user.target
```

![ConnectPrivate](/images/anh71.png)

- Kích hoạt và khởi động dịch vụ Node Exporter:

```bash
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
```

- Kiểm tra trạng thái của dịch vụ Prometheus:

```bash
sudo systemctl status node_exporter
```

![ConnectPrivate](/images/anh72.png)

{{% notice note %}}
Hãy nhớ tạo thêm một inbound rule cho phép truy cập vào port 9100 trên Security Group của server Monitoring.
{{% /notice %}}

![ConnectPrivate](/images/anh75.png)



