pipeline {
agent any
stages {
stage('chckout scm') {
steps {
checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/hellokaton/java11-examples.git']])
}  
}
stage('Install sonarqube cli') {
steps {
// Step to install SonarQube CLI
sh 'sudo apt install unzip -y'
sh 'sudo wget -O sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip'
sh 'sudo unzip -o -q sonar-scanner.zip'
sh 'sudo rm -rf /opt/sonar-scanner'
sh 'sudo mv --force sonar-scanner-5.0.1.3006-linux /opt/sonar-scanner'
sh 'sudo sh -c \'echo "#/bin/bash \nexport PATH=\\\"$PATH:/opt/sonar-scanner/bin\\\"" >/etc/profile.d/sonar-scanner.sh\''
sh 'sudo chmod +x /opt/sonar-scanner/bin/sonar-scanner'
sh '. /etc/profile.d/sonar-scanner.sh'
}
}
stage('Analyzing Code Quality') {
steps {
// Step to analyze code quality with SonarQube
sh '/opt/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=amitow1234_test -Dsonar.organization=amitow1234 -Dsonar.qualitygate.wait=false -Dsonar.qualitygate.timeout=300 -Dsonar.sources=src/main/java/ -Dsonar.java.binaries=target/classes -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=bb33f0779bb5343cceeb1301019798b7b57825ea'
}
}
    stage('Build') {
      steps {
        sh 'docker build -t my-flask-app .'
        }
        }
}
}
