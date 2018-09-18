node {
    dir("/home/jenkins/workspace/Hello-container"){
    checkout scm

    env.DOCKER_API_VERSION="1.23"
    appName = "default/flask-app"
    registryHost = "https://172.16.1.1:8500/"
    imageName = "${registryHost}${appName}:${env.BUILD_ID}"
    env.BUILDIMG=imageName
   /usr/bin/docker.withRegistry('https://172.16.1.1:8500/', 'admin'){
    stage "Build"

        def pcImg = /usr/bin/docker.build("https://172.16.1.1:8500/default/flask-app:${env.BUILD_ID}", "-f Dockerfile.ppc64le .")
        sh "cp /home/jenkins/workspace/Hello-container/.dockercfg ${HOME}/.dockercfg"
        pcImg.push()

    input 'Do you want to proceed with Deployment?'
    stage "Deploy"

        sh "kubectl set image deployment/demoapp-demochart demochart=${imageName}"
        sh "kubectl rollout status deployment/demoapp-demochart"
}
}
}

