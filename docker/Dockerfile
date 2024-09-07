# Build stage
FROM node:20-alpine AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Build the Next.js application
RUN npm run build

# Runtime stage
FROM node:20-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the built application from the build stage
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./
COPY --from=builder /app/node_modules ./node_modules

# Expose the port that the Next.js application will run on
EXPOSE 3000

# Define the command to run the Next.js application
CMD ["npm", "start"]