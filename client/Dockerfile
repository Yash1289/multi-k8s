 from node:16-alpine as builder

 workdir /app
 copy package.json .
 run npm install
 copy . .
 run npm run build

#This is the second base image that we are using after node image. This is the image that will be used to serve the build files.
#Using an alias builder for the first image so that we can refernce it and copy the build files from it to the second image.
#After running npm run build, the build files gets created inside our workdir /app/build. We are copying the build files from the first image to the second image using the copy command.
#In production environment we cannot port map like -p 8000:3000, instead we just write the port number that we want to expose in the dockerfile. In this case we are exposing port 80. 
#And our production deployment like AWS ECS will take care of the port mapping and routing the traffic to the container.
 from nginx:alpine
 Expose 3000
 #This activity is done to override the default port 80 of nginx with our port 3000. This is done because our react app is running on port 3000 and we want to serve it on the same port.
 copy ./nginx/default.conf /etc/nginx/conf.d/default.conf
 copy --from=builder /app/build /usr/share/nginx/html
