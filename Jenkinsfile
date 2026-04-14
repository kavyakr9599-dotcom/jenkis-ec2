pipeline {
    agent any

    stages {
        stage('Deploy') {
            steps {
                sshagent(['f7a63ef1-805b-4797-9aae-d341839e1c21']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@54.237.169.62 << EOF

                    echo "Connected to EC2"

                    cd /home/ubuntu

                    # Clone or pull repo
                    if [ -d "jenkis-ec2" ]; then
                        cd jenkis-ec2
                        git pull origin main
                    else
                        git clone https://github.com/Chigich/jenkis-ec2.git
                        cd jenkis-ec2
                    fi

                    echo "Code updated successfully"

                    EOF
                    '''
                }
            }
        }
    }
}
