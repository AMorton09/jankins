import hudson.FilePath
import groovy.json.JsonBuilder

stage 'CI'
node {

    checkout scm

    //git branch: 'jenkins2-course', 
    //    url: 'https://github.com/g0t4/solitaire-systemjs-course'

    // pull dependencies from npm
    // on windows use: bat 'npm install'
    sh 'npm install'

   
    // test with PhantomJS for "fast" "generic" results
    // on windows use: bat 'npm run test-single-run -- --browsers PhantomJS'
    sh 'npm run test-single-run -- --browsers PhantomJS'
    
    // archive karma test results (karma is configured to export junit xml files)
    step([$class: 'JUnitResultArchiver', 
          testResults: 'test-results/**/test-results.xml'])
          
}




def notify_kibana() {
node {
  stage("Testing Post") {
      json = "{ \"build\": { \"number\": \"lamp\", \"log\": \"log\", \"url\": \"lamp\", \"status\": \"lamp\", \"scm\": { \"culprits\": { }, \"changes\": { }, \"commit\": \"lamp\", \"url\": \"lamp\", \"branch\": \"lamp\" }, \"timestamp\": \"lamp\", \"notes\": \"\", \"artifacts\": { }, \"phase\": \"COMPLETED\", \"full_url\": \"lamp\", \"queue_id\": 0 }, \"display_name\": \"lamp\", \"name\": \"lamp\", \"url\": \"lamp\" }"
      sh "curl -X POST \"http://127.0.0.1:5000/API/Jenkins/Build\" -H \"Content-Type: application/json\" -d \"${json}\""
  }
}
                
// def COMMIT = bat (
//     script: 'git log',
//     returnStdout: true
// ).trim()
// bat "echo ${COMMIT}"
//def gitUrl = bat "git remote get-url origin"
//def scmUrl = scm.getUserRemoteConfigs()[0].getUrl()
//bat "echo" scmUrl"
//bat "curl -kX POST \"http://127.0.0.1:5000/API/Jenkins/Build\" -H \"Content-Type: application/json\" -d \"{\"build\": {\"number\": ${env.BUILD_NUMBER},\"log\": \"\",\"url\": \"${env.JOB_URL}\" ,\"status\": \"${currentBuild.currentResult}\", \"scm\": {\"culprits\": [],\"changes\": [], \"commit\": \"${scm.GIT_COMMIT}\", \"url\": \"lmap\", \"branch\": \"${scm.GIT_BRANCH}\", \"timestamp\": ${currentBuild.startTimeInMillis - currentBuild.duration},\"notes\": \"\",\"artifacts\": {},\"phase\": \"COMPLETED\",\"full_url\": \"${env.BUILD_URL}\",\"queue_id\": 0}},\"display_name\": \"${env.BUILD_DISPLAY_NAME}\",\"name\": \"${env.JOB_NAME}\",\"url\": \"job/\"}\""
//bat "curl -X POST \"http://127.0.0.1:5000/API/Jenkins/Build\" -H \"Content-Type: application/json\" -d \"${json}\"" 
}


stage 'Testing Post'
node{
    notify_kibana()
}







def notify(status){
    emailext (
      to: "wesmdemos@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
