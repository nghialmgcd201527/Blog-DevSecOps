---
title : "DevSecOps Pipeline"
weight : 1 
chapter : false
---
# DevSecOps Pipeline Project: Deploy ứng dụng với Amazon Elastic Kubernetes Service (EKS)

### Tổng quan

Với project này, chúng ta sẽ host ứng dụng bằng các dịch vụ của AWS. Mục tiêu chính là triển khai DevSecOps Pipeline cho ứng dụng bao gồm CI/CD sử dụng Jenkins, Monitoring sử dụng Prometheus và Grafana, Security sử dụng SonarQube và Trivy và cuối cùng là deploy ứng dụng lên Amazon Elastic Kubernetes Service (EKS) bằng ArgoCD và Helm.

![ConnectPrivate](/images/arc-log.png) 

### Nội dung

 1. [Giới thiệu](1-introduce/)
 2. [Các bước chuẩn bị](2-Prerequiste/)
 3. [Tạo kết nối đến máy chủ EC2](3-Accessibilitytoinstance/)
 4. [Quản lý session logs](4-s3log/)
 5. [Port Forwarding](5-Portfwd/)
 6. [Dọn dẹp tài nguyên](6-cleanup/)
