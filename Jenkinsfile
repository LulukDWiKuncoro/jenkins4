pipeline {
    agent any
    
    stages {
        stage('Deploy') {
            steps {
                echo "Simulating deploy from branch ${env.BRANCH_NAME}"
            }
        }
    }

    post {
        success {
            script {
                def payload = [
                    content: "✅ Build SUCCESS on '${env.BRANCH_NAME}' \nURL: ${env.BUILD_URL}"
                ]
                httpRequest(
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload),
                    url: 'https://canary.discord.com/api/webhooks/1425050964397654097/BM02GEfkw5Yh1IOoYiS4IbuEAKVz_GNKSjiqkOTuRGSoVcCDi-TD2mZJP0GhGimmsUc7'
                )
            }
        }

        failure {
            script {
                def payload = [
                    content: "❌ Build FAILED on '${env.BRANCH_NAME}' \nURL: ${env.BUILD_URL}"
                ]
                httpRequest(
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload),
                    url: 'https://canary.discord.com/api/webhooks/1425050964397654097/BM02GEfkw5Yh1IOoYiS4IbuEAKVz_GNKSjiqkOTuRGSoVcCDi-TD2mZJP0GhGimmsUc7'
                )
            }
        }
    }
}
