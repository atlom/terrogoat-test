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

                    echo "Downloading: $ASSET_URL"
                    curl -L "$ASSET_URL" -o .tools/terrascan.tar.gz

                    # Extrae todo y busca el binario
                    tar -xzf .tools/terrascan.tar.gz -C .tools
                    rm .tools/terrascan.tar.gz

                    # Asegura que exista el binario (suele estar en .tools/terrascan)
                    chmod +x .tools/terrascan

                    ./.tools/terrascan version

                '''
            }
        }
    }
}