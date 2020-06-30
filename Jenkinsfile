pipeline{
    environment{
        registry = "muditnaithani/docker-spring-boot-new"
        registryCredential = 'docker-creds'
        dockerImage = ''
    }
    agent any
    
    stages {
        stage ('Checkout SCM') {
                steps {
                git 'https://github.com/mudit-naithani/Java_Jenkins_Groovy_Pipeline.git'
                 }
               }
           
         
        stage ('Compile stage') {
                steps {
                    bat label: '', script: 'mvn clean install'
                }
            }
        
        /*
        stage ('Test') {
                steps {
                    bat label: '', script: 'mvn test'
                }
                post{
                        always{
                                 junit 'target/surefire-reports/*.xml'
                        }
                }
            }
        
        */
        
        /*
        stage ('OWASP Dependency-Check Vulnerabilities') {
            steps {
                dependencyCheck additionalArguments: ''' 
                    -o "./" 
                    -s "./"
                    -f "ALL" 
                    --prettyPrint''', odcInstallation: 'OWASP-DC'

                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
        */
        
        
        /*
        docker inspect <container name> --format="{{.NetworkSettings.Networks.nat.IPAddress}}"
        
        */
        
        
        stage ('Docker Build') {
                steps {
                    powershell label: '', script: 'docker stop docker-spring-boot-new-cont'
                    powershell label: '', script: 'docker rm docker-spring-boot-new-cont'
                    powershell label: '', script: 'dir $WORKSPACE'
                    powershell label: '', script: 'Copy-Item -Path C:\\Users\\muditn99\\.jenkins\\workspace\\Java_SpringBoot_Pipeline\\Dockerfile -Destination C:\\Users\\muditn99\\.jenkins\\workspace\\Java_SpringBoot_Pipeline\\target'
                    powershell label: '', script: 'Copy-Item -Path C:\\Users\\muditn99\\.jenkins\\workspace\\Java_SpringBoot_Pipeline\\test -Destination C:\\Users\\muditn99\\.jenkins\\workspace\\Java_SpringBoot_Pipeline\\target'
                    dir('C:\\Users\\muditn99\\.jenkins\\workspace\\Java_SpringBoot_Pipeline\\target') 
                    {
                    powershell label: '', script: 'dir $WORKSPACE'
                    script {
                    app = docker.build("muditnaithani/docker-spring-boot-new")
                    
                    //app= docker.image('muditnaithani/docker-spring-boot-new').withRun('-p 8085:8085')
                        
                    }
                    powershell label: '', script: 'docker run -d -p 8085:8085 --name "docker-spring-boot-new-cont" muditnaithani/docker-spring-boot-new'
                    //dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    
                    //powershell label: '', script: 'docker build -f Dockerfile -t docker-spring-boot .'
                    //sh label: '', script: 'docker build -f Dockerfile -t docker-spring-boot .'
                    //sh label: '', script: 'echo ${workspace}'
                    //sh label: '', script: 'echo pwd'
                    //dir('/target') 
                        
                    }
                        
                    }
				}
        
        
		/*
        
        stage ('Kubernetes Deploy') {
            steps {
                powershell label: '', script: 'dir $WORKSPACE'
                
                script{
                    //powershell label: '', script: 'kubectl version'
                    kubernetesDeploy configs: '.kube/config', kubeConfig: [path: ''], kubeconfigId: 'k8_master_config', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
                    //kubernetesDeploy(configs: "test", kubeconfigId: "k8_master_config")
                }
                //powershell label: '', script: 'kubectl create -f test'
            }
        }
        
        */
        
        
        stage ('Docker Push') {
                steps {
                    powershell label: '', script: 'dir $WORKSPACE'
                    script{
                        docker.withRegistry('https://registry.hub.docker.com', 'docker-creds')
                        {
                        //app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                        }
                    }
                    //script {
                    //docker.build("muditnaithani/docker-spring-boot-new")
                    //}
                    //dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    
                    //powershell label: '', script: 'docker build -f Dockerfile -t docker-spring-boot .'
                    //sh label: '', script: 'docker build -f Dockerfile -t docker-spring-boot .'
                    //sh label: '', script: 'echo ${workspace}'
                    //sh label: '', script: 'echo pwd'
                    //dir('/target') 
                        
                    }
                    
                    }
                
            }


}

