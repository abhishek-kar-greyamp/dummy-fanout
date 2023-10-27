node {
    stage('Build') {
        git branch: 'fix/non-blocking-start-scripts', url: 'https://github.com/abhishek-kar-greyamp/dummy-fanout.git'
        sh 'export PATH=$PATH:/usr/bin/npm' // Path to npm installation
        
        // Check for changes in the 'auth' folder
        if (changesInFolder('auth')) {
            sh 'npm run build'
            sh 'npm run start:auth'
        }
        
        // Check for changes in the 'user' folder
        if (changesInFolder('user_details')) {
            sh 'npm run build'
            sh 'npm run start:user'
        }
        //Check for changes in the 'product' folder
        if (changesInFolder('product_details')) {
            sh 'npm run build'
            sh 'npm run start:product'
        }
    }
}

def changesInFolder(folderName) {
    def changeLogSets = currentBuild.changeSets
    for (int i = 0; i < changeLogSets.size(); i++) {
        def entries = changeLogSets[i].items
        for (int j = 0; j < entries.length; j++) {
            if (entries[j].path.startsWith(folderName + '/')) {
                return true
            }
        }
    }
    return false
}
