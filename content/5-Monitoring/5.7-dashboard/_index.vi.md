---
title : "Tạo Dashboard"

weight : 7
chapter : false
pre : " <b> 5.7 </b> "
---

Quay lại giao diện chính của Grafana, chọn **DASHBOARDS**.

![ConnectPrivate](/images/anh80.png)

- Chọn **Import a dashboard**.

![ConnectPrivate](/images/anh84.png)

- Truy cập vào [Node Exporter Full](https://grafana.com/grafana/dashboards/1860-node-exporter-full/), chọn **Copy ID to clipboard**.

![ConnectPrivate](/images/anh85.png)

- Quay lại giao diện **Import a dashboard** của Grafana, dán ID vừa copy vào mục **Grafana.com Dashboard** và nhấn **Load**.

![ConnectPrivate](/images/anh86.png)

- Tại mục **Prometheus**, chọn Prometheus Data Source đã được thêm trước đó. Sau đó nhấn **Import**.

![ConnectPrivate](/images/anh87.png)

- Như vậy đã hoàn tất việc tạo Dashboard cho Node Exporter.

![ConnectPrivate](/images/anh88.png)

- Làm tương tự để tạo Dashboard cho Jenkins, đầu tiên chúng ta cần cài đặt Plugin cho Jenkins, sau đó restart lại Jenkins.

![ConnectPrivate](/images/anh89.png)

- Truy cập vào đường dẫn của Jenkins với path là `/prometheus` để kiểm tra xem Jenkins đã được Prometheus thu thập số liệu chưa.

![ConnectPrivate](/images/anh90.png)

- Làm tương tự như [bước cấu hình Prometheus thu thập metrics từ Node Exporter](/5-Monitoring/5.4-jkandprom/), chỉ cần chỉnh sửa file cấu hình `prometheus.yml` để cấu hình Prometheus thu thập thông tin của Jenkins.

![ConnectPrivate](/images/anh91.png)

- Kiểm tra các **Targets** đã được cấu hình trong Prometheus, chúng ta đã thêm thành công Jenkins vào Prometheus.

![ConnectPrivate](/images/anh92.png)

- Làm tương tự để import Dashboard cho Jenkins như dưới đây.

![ConnectPrivate](/images/anh93.png)

Vậy là đã tạo thành công hai dashboard cho Node Exporter và Jenkins trên Grafana.
















