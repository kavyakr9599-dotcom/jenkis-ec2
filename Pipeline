pipeline {
    agent any

    stages {
        stage('Deploy') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@54.237.169.62 << EOF

                    cd /home/ubuntu

                    if [ -d "app" ]; then
                        cd app && git pull
                    else
                        git clone https://github.com/Chigich/jenkis-ec2.git
                        cd app
                    fi

                    npm install
                    pm2 restart app || pm2 start app.js --name app

                    EOF
                    '''
                }
            }
        }
    }
}
