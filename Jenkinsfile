node {
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git 'https://github.com/UditSharma1632/jenkins.git'
        
    }
    stage('Build and Package') {
                bat "mvn clean package"
    }
     
    stage('Nexus') {
        nexusArtifactUploader artifacts: [[artifactId: 'spring-boot-starter-parent', classifier: '', file: 'target/jenkins-1.0.-SNAPSHOT.jar', type: 'jar']], credentialsId: 'nexus', groupId: 'org.springframework.boot',
            nexusUrl: 'localhost:8110', 
            nexusVersion: 'nexus3', protocol: 'http', 
            repository: 'nexusdeploymentrepo', version: '2.2.3.RELEASE'
    }
    
    stage('ansible') {
                ansiblePlaybook(credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible_master', inventory: 'inventory.inv', playbook: 'playbook.yml')
    }
}
