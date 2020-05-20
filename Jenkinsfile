node('slave'){
    stage('codeFetch') {
        container('jenkins-slave'){
            git branch: env.BRANCH_NAME, credentialsId: 'githubcredmaru', url: 'https://github.com/svvsmarutii/loansapp.git'
            container('maven') {
                stage('Build') {
                    configFileProvider([configFile(fileId: 'e15dea1f-e7d5-453e-aacf-ed6e5ac6c2ed', variable: 'MySettings')]) {
                        withEnv(['jobname=loansapp']) {
                            sh "mvn -s ${MySettings} clean install"
                         }
                        build job: 'testmultibranchpipeline/dev', propagate: false
                        sh 'find /root/.m2 -maxdepth 3 -type d'
                        sh 'du -sh /root/.m2'
                    }    
                }
            }
        }
    }
}
