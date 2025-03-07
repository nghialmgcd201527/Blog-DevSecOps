---
title : "Tích hợp Jenkins với Prometheus"

weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

Để cấu hình Prometheus thu thập số liệu từ Node Exporter, chỉ cần chỉnh sửa file cấu hình `prometheus.yml` như sau:

- Di chuyển tới thư mục chứ file cấu hình Prometheus:

```bash
cd /etc/prometheus
```

- Chỉnh sửa file cấu hình `prometheus.yml`:

```bash
sudo vi prometheus.yml
```

- Thêm cấu hình sau vào file:

```yaml
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['<your-node-exporter-ip>:<your-node-exporter-port>']
```

Như hình bên dưới.

![ConnectPrivate](/images/anh73.png)

- Lưu và thoát file cấu hình. Kiểm tra xem cấu hình đã phù hợp chưa bằng cách chạy lệnh:

```bash
promtool check config /etc/prometheus/prometheus.yml
```

![ConnectPrivate](/images/anh74.png)

- Reload cấu hình Prometheus mà không cần phải restart dịch vụ:

```bash
curl -X POST http://localhost:9090/-/reload
```

- Truy cập giao diện Prometheus và kiểm tra xem số liệu từ Node Exporter đã được thu thập chưa.

![ConnectPrivate](/images/anh76.png)







