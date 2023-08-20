FROM node:18.10-alpine AS build
WORKDIR /app
RUN npm install -g @angular/cli
COPY package.json package-lock.json ./
RUN npm install
COPY . .
ARG configuration=production
RUN npm run build -- --output-path=./dist/out --configuration $configuration

#FROM nginx:latest

# Copy the build output to replace the default nginx contents.
#COPY --from=build /usr/local/app/dist/client /usr/share/nginx/html
FROM nginx:latest
# Copying compiled code and nginx config to different folder
# NOTE: This path may change according to your project's output folder 
COPY --from=build /app/dist/out/ /usr/share/nginx/html
COPY ./nginx-custom.conf /etc/nginx/conf.d/default.conf
# Exposing a port, here it means that inside the container 
# the app will be using Port 80 while running

# Expose port 80
#EXPOSE 80
#CMD ["ng", "serve", "--host", "0.0.0.0"]
