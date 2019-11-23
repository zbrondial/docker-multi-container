# Use an existing image as a base from hub.docker.com
FROM node:alpine as builder

# Specifying a work directory 
WORKDIR /app

# Copying build files into the container
# Download and install dependency

COPY ./package.json ./
RUN npm config set registry https://registry.npmjs.org/
RUN npm install
COPY ./ ./

# Tell the image what to do when it starts as a container
RUN ["npm","run","build"]

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html