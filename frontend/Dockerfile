FROM node:16-alpine
# The /app directory should act as the main application directory
WORKDIR /app
COPY . .
RUN npm install
ENV ENDPOINT http://localhost:9000/api
EXPOSE 8000
# Start the app
CMD [ "npm", "start"]
