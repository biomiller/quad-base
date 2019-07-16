pipeline{
        agent any
        stages{
		stage('---build---'){
                        steps{
                                sh "sudo docker-compose build server client"
                        }
                }
		 stage('---push---'){
                        steps{
                                sh "sudo docker push biomiller/quad-server"
                                sh "sudo docker push biomiller/quad-client"
                        }
                }
		stage('---patches---'){
                        steps{
                                sh "kubectl patch deployment server -p "{\"spec\":{\"template\":{\"metadata\":{\"labels\":{\"date\":\"`date +'%s'`\"}}}}}""
				sh "kubectl patch deployment client -p "{\"spec\":{\"template\":{\"metadata\":{\"labels\":{\"date\":\"`date +'%s'`\"}}}}}""

                        }
                }
		stage('---apply_server ---'){
                        steps{
                                sh "kubectl apply -f server/"
                        }
                }
		stage('---apply_client ---'){
                        steps{
                                sh "kubectl apply -f client/deployment.yaml"
                                sh "kubectl apply -f client/service.yaml"
                        }
                }
        }
}
