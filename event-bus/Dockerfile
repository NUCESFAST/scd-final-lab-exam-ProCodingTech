# Use an official Node.js runtime as the base image
FROM node:14


# Set the working directory in the container
WORKDIR /i211133_eventbus


# Copy package.json and package-lock.json to the working directory
COPY package*.json ./


# Install dependencies
RUN npm install


# Copy the rest of the application code to the working directory
COPY . .


# Expose the port your app runs on
EXPOSE 3331


# Command to run the application
CMD ["npm", "start"]