FROM node:16-alpine
# The /app directory should act as the main application directory
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 9000
# Start the app
CMD [ "npm", "run", "dev" ]