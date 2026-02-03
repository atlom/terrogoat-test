pipeline{
    agent any
    stages{
        stage ('terrascan'){
            steps{
                sh '''
                    apk add --no-cache curl tar

                    curl -L "$(curl -s https://api.github.com/repos/tenable/terrascan/releases/latest | grep -o -E "https://.+?_Linux_x86_64.tar.gz")" > terrascan.tar.gz
                    tar -xf terrascan.tar.gz terrascan && rm terrascan.tar.gz
                    sudo install terrascan /usr/local/bin && rm terrascan
                    terrascan 

                '''
            }
        }
    }
}