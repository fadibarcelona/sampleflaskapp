node ('dbnode') {
    dir("/home/gkepoc_gmail_com"){
    checkout scm
    sh "sudo su -"
    env.DOCKER_API_VERSION="1.23"
    appName = "default/flask-app"
    registryHost = "gcr.io/coastal-antler-216919/"
    imageName = "${registryHost}${appName}:${env.BUILD_ID}"
    env.BUILDIMG=imageName
    docker.withRegistry('gcr.io/coastal-antler-216919/'){
    stage "Build"
         sh "sudo su -"
        def pcImg = docker.build("gcr.io/coastal-antler-216919/default/flask-app:${env.BUILD_ID}", "-f Dockerfile.ppc64le .")
        sh "cp /home/gkepoc_gmail_com/.dockercfg /home/gkepoc_gmail_com/.dockercfg"
        pcImg.push()

    input 'Do you want to proceed with Deployment?'
    stage "Deploy"
        sh "sudo su -"
        sh "kubectl set image deployment/demoapp-demochart demochart=${imageName}"
        sh "kubectl rollout status deployment/demoapp-demochart"
}
}
}

