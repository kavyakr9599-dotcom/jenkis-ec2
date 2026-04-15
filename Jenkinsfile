pipeline {
    agent any

    stages {
        stage('Deploy Nginx App') {
            steps {
                sshagent(['b7a1f921-2c73-45bd-9d0e-954504ea436a']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@16.171.15.248<< 'EOF'

                    cd /home/ubuntu

                    # Clone or pull repo
                    if [ -d "jenkis-ec2" ]; then
                        cd jenkis-ec2
                        git pull origin main
                    else
                        git clone https://github.com/HarshithNA/jenkis-ec2
                        cd jenkis-ec2
                    fi

                    # Build Docker image
                    docker build -t my-nginx-app .

                    # Stop old container
                    docker rm -f nginx-container || true

                    # Run new container
                    docker run -d -p 80:8081 --name nginx-container my-nginx-app

                    echo "Nginx app deployed"

EOF
                    '''
                }
            }
        }
    }
}
