# Weatherapp

There was a beautiful idea of building an app that would show the upcoming weather. The developers wrote a nice backend and a frontend following the latest principles and - to be honest - bells and whistles. However, the developers did not remember to add any information about the infrastructure or even setup instructions in the source code.

Luckily we now have [docker compose](https://docs.docker.com/compose/) saving us from installing the tools on our computer, and making sure the app looks (and is) the same in development and in production. All we need is someone to add the few missing files!

## Approach

*Use Docker Compose to deploy application locally.
*Use Ansible to setup docker, docker compose, and run application on AWS EC2 Instance.
*Use container orchestration tool ECS to deploy app.
*Use CI/CD GitHub Actions to deploy to ECS and update services.

## Run Application Locally
*Clone Repo 
*Update APPID with api key from http://openweathermap.org
*Go to backend and frontend folders and run app using `npm i && npm start` or 
*For running in docker use command `docker-compose up -d --build`. It will build your docker container and also start them.
*Go to browser Backend will be at: `http:localhost:9000/api/weather` and Frontend will be at `http:localhost:8000`


## Ansible + Cloud Deployment
*Clone Repo
*Install ansible in your local machine and make sure you can SSH to EC2 machine where app needs to be deployed
*Go to ansible/chapter1 folder and update 
*SSH key location in ansible.cfg and EC2 public IP in inventory and playbook
*Deploy to EC2 using comand `ansible-playbook playbook.yml`
*This will deploy your app to EC2. Hit public IP on browser to view app `http:<publicip>:8000` 

## ECS + GitHub Actions Deployment
*Create ECS Cluster and make ECR repo and ECS Task Defintion for frontend and backend Container.
*Launch Services in ECS cluster for both containers and use laod balncer to expose services and intercommunication
*Hit Frontend LoadBalancer URL on browser at port 8000
*GitHub Action are triggered on every push to main branch and does following steps: Docker build -> Push to ECR -> Update ECS Services
*Build docker images for frontend and backend
*Push new images to ECR
*Update services in ECS cluster to use new image
*And BOOM! you have CI/CD pipelines for your app. Cool.

## AWS Deployments URL
*EC2: Backend `http://13.48.24.249:9000/api/weather` Frontend: `http://13.48.24.249:8000`
*ECS: Backend ALB `http://backendlb-1704120884.eu-north-1.elb.amazonaws.com:9000/api/weather` Frontend: `http://frontendlb-1879494820.eu-north-1.elb.amazonaws.com:8000`