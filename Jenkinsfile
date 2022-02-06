//gitlab的凭证
def git_auth = "endeavor"
//构建版本的名称
def tag = "latest"
//Harbor私服地址
def harbor_url = "192.168.174.101:85/tensquare/"

node {
    stage('拉取源代码') {
        checkout([$class: 'GitSCM', branches: [[name: "*/${branch}"]], extensions: [], userRemoteConfigs: [[credentialsId: "${git_auth}", url: 'git@github.com:endeavor66/tensquare_back.git']]])
    }
    stage('代码审查') {
        def scannerHome = tool 'sonarqube-scanner'
        withSonarQubeEnv('sonarqube') {
            sh """
            cd ${project_name}
            ${scannerHome}/bin/sonar-scanner
            """
        }
    }
    stage('编译，构建镜像') {
        //定义镜像名称
        def imageName = "${project_name}:${tag}"
        //编译，安装公共工程
        sh "mvn -f tensquare_common clean install"
        //编译，构建本地镜像
        sh "mvn -f ${project_name} clean package dockerfile:build"
    }
}