pipeline
{
    agent any
    
    triggers{
        githubPush()
    }

    environment
    {
        NGINX_IP = "13.61.15.247"
        NGINX_USER = "ec2-user"
    }

    stages{
        // stage('Clone Repository')
        // {
        //     steps
        //     {
        //         git "https://github.com/mayurthitame/static-web-app.git"
        //     }
        // }

        stage('Upload to nginx  server')
        {
            steps
            {
                  sshagent(['TomcatServer_SSH_Credentials']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${NGINX_USER}@${NGINX_IP} sudo rm -rf /usr/share/nginx/html/* || true
                        scp -o StrictHostKeyChecking=no -r * ${NGINX_USER}@${NGINX_IP}:/usr/share/nginx/html/
                    """
                }
            }
        }
    }
}