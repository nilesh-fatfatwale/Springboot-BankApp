pipeline{
    agent any;
    
    stages{
        stage ("clone"){
            steps {
                git url : "https://github.com/nilesh-fatfatwale/Springboot-BankApp.git" , branch : "main"
            }
        }
        stage("build"){
            steps {
                sh "docker build -t bankapp-eks:v2 ."
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockerHub",
                    usernameVariable: "dockerHubUser",
                    passwordVariable: "dockerHubPass")]){
                sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                sh "docker image tag bankapp-eks:v2 nileshfatfatwale/bankapp-eks:v2"
                sh "docker push nileshfatfatwale/bankapp-eks:v2"
                    }
            }
        }
    }
}
