# Use Node.js 20 (matches Jenkins setup)
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy package files first (caching optimization)
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy app source
COPY . .

# Expose port 
EXPOSE 3000

# Start command
CMD ["npm", "start"]