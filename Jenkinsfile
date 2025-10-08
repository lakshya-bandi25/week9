pipeline{
	agent any
	stages{
	stage('Build'){
	steps{
	echo "Build Docker Image"
	bat "docker build -t mypythonflaskapp ."
	}
	}
	stage('Run'){
	steps{
	echo "Run application in Docker Container"
	bat "docker rm -f mycontainer || exit 0"
	bat "docker run -d -p 5000:5000 --name mycontainer mypythonflaskapp"
	}
	}
	}
	post{
	success{
	echo 'Pipeline completed successfully!'
	}
	failure{
	echo 'Pipeline failed.Please check the logs'
	}
	
	}
}pipeline{
    agent any
    stages{
        stage("Build Docker image"){
            steps{
                echo "Build Docker image"
                bat "docker build -t kubdemoapp:v1 ."
            }
        }
        stage("Docker Login"){
            steps{
                bat "docker login -u lakshyabandi25 -p Lakshya.bandi"
            }
        }
        stage("push Docker image to docker hub"){
            steps{
                echo "push Docker image to docker hub"
                bat "docker tag kubdemoapp:v1 lakshyabandi25/week8:t1"
                bat "docker push lakshyabandi25/week8"
            }
        }
        stage("Deploy to kubernetes"){
            steps{
                echo "Deploy to kubernetes"
                bat "kubectl apply -f deployment.yaml --validate=false"
                bat "kubectl apply -f service.yaml"
            }
        }
    }
    post{
        success{
            echo "Pipeline executed successfully"
        }
        failure{
            echo "pipeline failed.Please check the logs"
        }
    }
}
