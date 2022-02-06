//gitlab的凭证
def git_auth = "endeavor"
node {
    stage('pull code') {
        checkout([$class: 'GitSCM', branches: [[name: "*/${branch}"]], extensions: [], userRemoteConfigs: [[credentialsId: "${git_auth}", url: 'git@github.com:endeavor66/tensquare_back.git']]])
    }
}