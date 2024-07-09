# build-with-docker


# Steps I followed to build an Image and Push to ECR

- Create a Dockerfile
- write the Build Instructions
- make sure your html files are in the same directory as your Dockerfile(Build Context)
- command to build : `docker build -t krupa-web-app .`
- Tag this image to your accountname/repository name: `docker tag krupa-web-app:latest 975050204585.dkr.ecr.us-east-1.amazonaws.com/krupa-web-app:latest`
- once tagged, if you try to push the image, it fails because you're not authenticated to push to ECR.
- to login to ECR ` aws ecr get-login-password | docker login -u AWS --password-stdin "https://$(aws sts get-caller-identity --query 'Account' --output text).dkr.ecr.us-east-1.amazonaws.com`
- in order to successfully login to ECR using above command, you have to set up local AWS CLI and configure with AWS IAM user Access Keys.
- Push Command `docker push 975050204585.dkr.ecr.us-east-1.amazonaws.com/krupa-web-app:latest`



# issues I faced during multiple code changes and building Images


- when I update my webpage and rebuild image, the new changes were not reflected in the new image as the docker caches layers.
- To ensure that your Docker image is always built with the latest version of your webpage files, you can use a strategy that forces Docker to invalidate the cache for those specific files.
- command I used to invalidate cache `docker build --no-cache -t krupa-web-app:no-cache .`
`
