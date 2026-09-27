node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace') {
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo') {
        echo 'Cloning the Repository'

        git(
            branch: 'main',
            url: 'https://github.com/Yash-978/CICI-Jenkins-AWS'
        )
    }

    stage('Deploy to EC2') {
        echo 'Deploying to EC2'

        sh """
            sudo mkdir -p ${appDir}

            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete \
                --exclude='.git' \
                --exclude='node_modules' \
                ./ ${appDir}/

            cd ${appDir}

            npm install

            npm run build

            sudo fuser -k 3000/tcp || true

            nohup npm run start > /tmp/nextjs.log 2>&1 &
        """
    }
}