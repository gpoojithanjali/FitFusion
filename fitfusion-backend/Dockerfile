# Use official Node.js image
FROM node:23-alpine-slim

# Create app directory
WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy rest of the app
COPY . .

# Expose port (if using 3000)
EXPOSE 3000

# Run the server
CMD ["node", "index.js"]
