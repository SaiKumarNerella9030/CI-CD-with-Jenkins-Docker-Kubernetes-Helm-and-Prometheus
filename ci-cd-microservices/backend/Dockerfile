FROM node:18-alpine
WORKDIR /app
COPY app.js .
RUN npm install express
EXPOSE 5000
CMD ["node", "app.js"]
