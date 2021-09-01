**My plan is createto host React App in docker**

Brief about React :
*React is a free and open-source front-end JavaScript library for building user interfaces or UI components. It is maintained by Facebook and a community of individual developers and companies. React can be used as a base in the development of single-page or mobile applications*

## Docker file - Create docker "Dockerfile" and store followings in it

> **#Stage 1**
> 
> FROM node:10-alpine as build-step
> 
> RUN mkdir /app
> 
> WORKDIR /app
> 
> COPY package.json /app
> 
> RUN npm install
> 
> COPY . /app RUN npm run build
> 
>  **#Stage 2** 
> FROM nginx:1.17.1-alpine 
> COPY --from=build-step /app/build /usr/share/nginx/html

## Explanation 

 - In **Stage 1**, we are copying our app code in the “app” folder and installing app dependencies from package.json file and creating production build using Node image.
-  In the **Stage 2**, we are using nginx server image to create nginx server and deploy our app on it by copying build items from */app/build* folder to nginx server at */usr/share/nginx/html* location.
  
### **Create a Docker Image**

Run the Docker build command to build Docker image of our app using Dockerfile that we have just created.
Note that I have given  m20aie287/react-app  as name to my Docker image 

Also, note that image name must be followed by the dot(.) which means that the path of the Docker build context and Dockerfile is the current folder.

`$ docker build -t m20aie287/react-app .`

Once docker image is created , we use following command to see all available images

> docker images
### **Run the Docker Container**

Run the following command in the terminal to run your ReactJS Todo App in the Docker container 

`$ docker run -d -it -p 80:80/tcp --name react-app m20aie287/react-app:latest`

