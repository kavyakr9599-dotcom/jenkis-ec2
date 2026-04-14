pipeline {
    agent any

    stages {
        stage('Deploy') {
            steps {
                sshagent(['f7a63ef1-805b-4797-9aae-d341839e1c21']) {
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
