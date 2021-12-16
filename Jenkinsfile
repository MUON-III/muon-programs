pipeline {
  agent {
    label '!windows-1' 
  }
  environment {
    CASM_URL = 'https://jenkins.i-am.cool/job/muon-casm/job/master/44/artifact/casm-static-d9a7235-git' 
  }
  stages {
    stage('Assemble muon-echotest') {
      steps {
        sh 'curl -L "$CASM_URL" -o casm-static && chmod +x casm-static'
        dir("build"){
          sh '$WORKSPACE/casm-static --input $WORKSPACE/echotest.txt --output muon-echotest.rom'
          archiveArtifacts artifacts: 'muon*', fingerprint: true
          deleteDir()
        }
      }
    }
  }
  
  post {
      cleanup { 
          cleanWs() 
      }
  }
}

