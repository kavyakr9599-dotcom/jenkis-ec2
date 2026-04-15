pipeline {
    agent any

    stages {
        stage('Deploy Nginx App') {
            steps {
                sshagent(['41acdb23-f798-4c7c-86d1-3126b5f82bda']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@98.94.82.118<< 'EOF'

                    cd /home/ubuntu

                    # Clone or pull repo
                    if [ -d "jenkis-ec2" ]; then
                        cd jenkis-ec2
                        git pull origin main
                    else
                        https://github.com/kavyakr9599-dotcom/jenkis-ec2.git
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
