FROM node:12.18.1

# The /app directory should act as the main application directory
WORKDIR /app
COPY . .
RUN npm install

# Start the app
CMD [ "npm", "run", "dev" ]

