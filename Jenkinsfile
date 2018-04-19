node {
    
    notify('Started')
    try {
        stage('checkout'){
            git 'https://github.com/g0t4/jenkins2-course-spring-petclinic.git'
        }
        
        stage('compiling, test, packaging'){
            sh 'mvn clean verify'
        }
        
        notify('Success')
    } catch (err) {
        notify("Error ${err}")
        currentBuild.result = 'FAILURE'
    }
    
    stage('archival'){
            junit 'target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.?ar' 
        }
    
}

def notify(status){
    emailext (
      to: "svoitenko@griddynamics.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
