node('master') {
    def myMavenContainer = docker.image('maven')
    myMavenContainer.pull()

    stage('checkout scm') {
        checkout([$class: 'GitSCM', 
		branches: [[name: '*/master']], 
		doGenerateSubmoduleConfigurations: false, 
		extensions: [[$class: 'CleanCheckout']], 
		submoduleCfg: [], 
		userRemoteConfigs: [[credentialsId: 'github_credentials', url: 'https://github.com/syamv/jenkinstest.git']]])
    }

    stage('maven build') {
      myMavenContainer.inside() {
        sh 'mvn clean install -Dmaven.test.skip=true'
		}
    }
}
