node {
    def appDir = '/var/www/jextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspaces'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'Cloning the Repo'
        git(
            branch: 'main',
            url: 'https://github.com/Yash-978/CICI-Jenkins-AWS'
        )
    }

    stage('Deploy to EC2'){
        echo 'Deploying to EC2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='.node_modules' .
            / ${appDir}

            cd ${appDir}
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp || true
            npm run start

        """
    }
}