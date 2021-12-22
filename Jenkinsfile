node {
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git 'https://github.com/UditSharma1632/jenkins.git'
        
    }
    stage('Build and Package') {
                bat "mvn clean package"
    }
     
    stage('Nexus') {
        nexusArtifactUploader artifacts: [[artifactId: 'jenkins', classifier: '', file: 'target/jenkins-1.0.0-SNAPSHOT.jar', type: 'jar']], 
            credentialsId: 'jenkins', groupId: 'com.maven.demo', nexusUrl: 'localhost:8110', nexusVersion: 'nexus3', 
            protocol: 'http', repository: 'nexus-repo', version: '1.0.0'
    }
    
    stage('ansible') {
                ansiblePlaybook(credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible_master', inventory: 'inventory.inv', playbook: 'playbook.yml')
    }
}
