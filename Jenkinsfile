pipeline{
    agent any
    stages{
        stage("scm"){
            steps{
               git credentialsId: 'github', url: 'https://github.com/aravinth99/git_3.git'
            }
        }
       
        stage("k8s_deploy"){
                steps{
                    sshagent(['k8s_key']) {
                        sh "scp -o StrictHostKeyChecking=no secret.yaml  vmubuntu@192.168.56.101:/home/vmubuntu/"
                        
                        script{
                            kubernetesDeploy(configs: "secret.yaml", kubeconfigId: "k8s-config")
                        }
                }
            }
        }
    }
}
