// pipeline {
//     agent {
//         docker {
//             image 'maven:3.9.0'
//             args '-v /root/.m2:/root/.m2'
//         }
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'mvn -B -DskipTests clean package'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh 'mvn test'
//             }
            // post {
            //     always {
            //         junit 'target/surefire-reports/*.xml'
            //     }
            // }
//         }
//     }
// }

node {
    docker.image('maven:3.9.0').inside('-v /root/.m2:/root/.m2') {
        stage('Build') {
            echo "Builded with Scripted Pipeline"
            sh 'mvn -B -DskipTests clean package'
            }
        stage('Test') { 
            echo "Tested with Scripted Pipeline"
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml' 
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?'
        }
        stage('Deliver') { 
            sh './jenkins/scripts/deliver.sh'
            sleep(time: 1, unit: 'MINUTES')
        }
    }
}
