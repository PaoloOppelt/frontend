# Build step: build the React frontend
FROM node:14-alpine as build-step
WORKDIR /app
COPY package*.json ./
COPY ./frontend ./frontend
RUN cd frontend && npm install && npm run build

# Serve the built React app using a static server
FROM node:14-alpine
WORKDIR /app
# Install serve to serve the static files
RUN npm install -g serve
# Copy the built app from the previous step
COPY --from=build-step /app/frontend/build /app
# Expose the port that serve will use (default is 5000, but you can set it to 10000 for Render)
EXPOSE 10000
# Command to serve the app
CMD ["serve", "-s", ".", "-l", "10000"]
