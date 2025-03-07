---
title : "Khởi tạo Jenkins pipeline"

weight : 10
chapter : false
pre : " <b> 4.10 </b> "
---

Truy cập giao diện chính của Jenkins, chọn **New Item** -> **Pipeline**. Đặt tên cho pipeline là `DevSecOps`, chọn **OK**.

![ConnectPrivate](/images/anh51.png)

Cuộn xuống mục **Pipeline** và copy Pipeline script dưới đây vào mục **Script**.

```groovy
pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/nghialmgcd201527/Workshop-DevSecOps.git'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=DevSecOps \
                    -Dsonar.projectKey=DevSecOps '''
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-token' 
                }
            } 
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        stage('OWASP FS SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){   
                       sh "docker build -t devsecops ."
                       sh "docker tag devsecops nghialmgcd201527/devsecops:latest "
                       sh "docker push nghialmgcd201527/devsecops:latest "
                    }
                }
            }
        }
        stage("TRIVY"){
            steps{
                sh "trivy image nghialmgcd201527/devsecops:latest > trivyimage.txt" 
            }
        }
        stage('Deploy to container'){
            steps{
                sh 'docker run -d --name devsecops -p 8081:3000 nghialmgcd201527/devsecops:latest'
            }
        }
    }
}
```

Nhấn **Apply** và **Save** để lưu cấu hình. Tại trang của pipeline, nhấn **Build Now** để chạy pipeline.

![ConnectPrivate](/images/anh53.png)

Truy cập vào **Pipeline Overview** để xem tiến trình của pipeline.

![ConnectPrivate](/images/anh54.png)

Nếu các bạn gặp lỗi **docker login failed** như dưới đây. 

![ConnectPrivate](/images/anh55.png)

Hãy kiểm tra lại thông tin credential của Docker Hub đã được cấu hình đúng chưa, nếu đúng rồi thì hãy cấp quyền cho Jenkins chạy Docker và khởi động lại Jenkins để áp dụng cấu hình mới.

```bash
sudo su
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

Hãy thử chạy lại pipeline và kiểm tra kết quả.

![ConnectPrivate](/images/anh57.png)


Sau khi pipeline chạy xong, truy cập vào giao diện quản lí repository của Docker Hub để kiểm tra xem image đã được push lên chưa.

![ConnectPrivate](/images/anh58.png)


Và kiểm tra ở SonarQube những issues được phát hiện.

![ConnectPrivate](/images/anh59.png)

Vậy là đã thành công bước set up Jenkins Pipeline, bây giờ đến phần Monitoring.













