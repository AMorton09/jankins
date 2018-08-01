
pipeline {
    agent none 
    stages {

stage ('CI'){


    checkout scm

    //git branch: 'jenkins2-course', 
    //    url: 'https://github.com/g0t4/solitaire-systemjs-course'

    // pull dependencies from npm
    // on windows use: bat 'npm install'
    bat 'npm install'

    // stash code & dependencies to expedite subsequent testing
    // and ensure same code & dependencies are used throughout the pipeline
    // stash is a temporary archive
    stash name: 'everything', 
          excludes: 'test-results/**', 
          includes: '**'
    
    // test with PhantomJS for "fast" "generic" results
    // on windows use: bat 'npm run test-single-run -- --browsers PhantomJS'
    bat 'npm run test-single-run -- --browsers PhantomJS'
    
    // archive karma test results (karma is configured to export junit xml files)
    step([$class: 'JUnitResultArchiver', 
          testResults: 'test-results/**/test-results.xml'])
          


// demoing a second agent

    // on windows use: bat 'dir'
    bat 'dir'

    // on windows use: bat 'del /S /Q *'
    bat 'del /S /Q *'

    unstash 'everything'

    // on windows use: bat 'dir'
    bat 'dir'


}

//parallel integration testing
stage ('Browser Testing'){
parallel chrome: {
    runTests("Chrome")
}





    bat 'echo TEST'


input 'Deploy to staging?'
}
// limit concurrency so we don't perform simultaneous deploys
// and if multiple pipelines are executing, 
// newest is only that will be allowed through, rest will be canceled
stage name: 'Deploy to staging', concurrency: 1

    bat 'echo TEST'

    }}

post { 
        always { 
            bat 'echo kibana post sent?'
            notify_kibana()
        }
    }





def notify_kibana() {
sh 'curl -X POST "http://127.0.0.1:5000/API/Jenkins/Build" -H "Content-Type: application/json" -d" {{"build": {"number": $ { env.BUILD_NUMBER },"log": "","url": $ {env.JOB_URL},"status": $ {currentBuild.currentResult},   "scm": {"culprits": [],"changes": [],    "commit": $ {     scm.GIT_COMMIT    },    "url": $ {     scm.GIT_URL    },    "branch": $ {     scm.GIT_BRANC         },    "timestamp": $ {     currentBuild.startTimeInMillis - currentBuild.duration},"notes": "","artifacts": {},"phase": "COMPLETED","full_url": $ {     env.BUILD_URL    },    "queue_id": 0},"display_name": $ {env.BUILD_DISPLAY_NAME},"name": $ {env.JOB_NAME},"url": "job/" + $ {env.BUILD_DISPLAY_NAME} + "/" + $ {    env.BUILD_NUMBER}  } } " '
}



def runTests(browser) {
    
        // on windows use: bat 'del /S /Q *'
        bat 'del /S /Q *'

        unstash 'everything'

        // on windows use: bat "npm run test-single-run -- --browsers ${browser}"
        bat "npm run test-single-run -- --browsers ${browser}"

        step([$class: 'JUnitResultArchiver', 
              testResults: 'test-results/**/test-results.xml'])
    
}

def notify(status){
    emailext (
      to: "wesmdemos@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
