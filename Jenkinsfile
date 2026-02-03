pipeline{
    agent {
        docker{
            image 'python:3.11-alpine'
        }
    }
    stages{
        stage ('terrascan'){
            steps{
                sh '''
                    apk add --no-cache curl tar

                    set -e
                    mkdir -p .tools reports

                    ASSET_URL=$(curl -s https://api.github.com/repos/tenable/terrascan/releases/latest \
                        | grep -Eo 'https://[^"]+_Linux_x86_64\\.tar\\.gz' | head -n 1)

                    curl -L "$ASSET_URL" -o .tools/terrascan.tar.gz

                    tar -xzf .tools/terrascan.tar.gz -C .tools
                    rm .tools/terrascan.tar.gz

                    chmod +x .tools/terrascan

                    ./.tools/terrascan scan -i terraform -d terragoat -o json > reports/terrascan.json

                '''
            }
        }
    }
}