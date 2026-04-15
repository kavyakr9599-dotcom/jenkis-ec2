pipeline {
    agent any

    stages {
        stage('Deploy Nginx App') {
            steps {
                sshagent(['554c1d0c-6228-4462-a05e-d0470ac10300']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@54.237.169.62 << 'EOF'

                    cd /home/ubuntu

                    # Clone or pull repo
                    if [ -d "jenkis-ec2" ]; then
                        cd jenkis-ec2
                        git pull origin main
                    else
                        git clone https://github.com/Chigich/jenkis-ec2.git
                        cd jenkis-ec2
                    fi

                    # Build Docker image
                    docker build -t my-nginx-app .

                    # Stop old container
                    docker rm -f nginx-container || true

                    # Run new container
                    docker run -d -p 80:80 --name nginx-container my-nginx-app

                    echo "Nginx app deployed"

EOF
                    '''
                }
            }
        }
    }
}
