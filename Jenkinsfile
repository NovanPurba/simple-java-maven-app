node {
    checkout scm
    docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2') {
        stage('Build'){
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test'){
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
        stage('Delivery'){
            sh './jenkins/scripts/deliver.sh'
            
        } 
        stage('Manual Approval'){
            input message: 'Lanjutkan ke tahap Deploy?' 
            echo "Mohon tunggu"
            
        } 
        stage('Deploy'){
            echo "Deploying App"
            sleep(time: 1, unit: 'MINUTES')
        }
    }
}