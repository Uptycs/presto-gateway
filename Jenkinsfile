pipeline {
    agent { label 'uptycsu20' }
    stages  {
        stage('Maven Build') {
            steps {
                script {
                    docker.image('maven:3.6.3-jdk-11').inside('--network host') {
                        sh 'mvn clean package -DskipTests'
                    }
                }
            }
        }
        stage('Upload Jar to S3') {
            steps {
                sh 'aws s3 cp gateway-ha/target/gateway-ha-1.9.5-jar-with-dependencies.jar s3://uptycs-builds-2/presto-gateway/gateway-ha-1.9.5-jar-with-dependencies.jar --acl bucket-owner-full-control'
            }
        }
    }
}
