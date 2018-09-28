node {
    dir("/home/gkepoc_gmail_com"){
    checkout scm

    env.DOCKER_API_VERSION="1.23"
    appName = "default/flask-app"
    registryHost = "gcr.io/coastal-antler-216919/"
    imageName = "${registryHost}${appName}:${env.BUILD_ID}"
    env.BUILDIMG=imageName
    docker.withRegistry('gcr.io/coastal-antler-216919/', 'docker'){
    stage "Build"

        def pcImg = docker.build("gcr.io/coastal-antler-216919/default/flask-app:${env.BUILD_ID}", "-f Dockerfile.ppc64le .")
        sh "cp /home/gkepoc_gmail_com/.dockercfg ${HOME}/.dockercfg"
        pcImg.push()

    input 'Do you want to proceed with Deployment?'
    stage "Deploy"

        sh "kubectl set image deployment/demoapp-demochart demochart=${imageName}"
        sh "kubectl rollout status deployment/demoapp-demochart"
}
}
}

