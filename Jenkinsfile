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
        stage('Clone Repository')
        {
            steps
            {
                git "https://github.com/mayurthitame/static-web-app.git"
            }
        }

        stage('Upload to nginx  server')
        {
            steps
            {
                sh """
                    //remove existing files
                    ssh -o StrictHostKeyChecking=no ${NGINX_USER}@${NGINX_IP} rm -rf /usr/share/nginx/html/*
                    scp -o StrictHostKeyChecking=no -r * ${NGINX_USER}@${NGINX_IP}:/usr/share/nginx/html/
                """
            }
        }
    }
}