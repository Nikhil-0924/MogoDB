# MogoDB

1. Verify MongoDB is Running

# Using Docker CLI
Check if the MongoDB container is running:

 docker ps
 
Look for a container with an image like mongo:latest and note its CONTAINER ID.

# Check MongoDB Logs
View the MongoDB logs to ensure it started successfully:

docker logs <container_id>

2. Connect to MongoDB

Option A: Use MongoDB CLI Inside the Container
Open a shell session inside the MongoDB container:

docker exec -it <container_id> mongosh

Replace <container_id> with the MongoDB container's ID or name.

Authenticate with the credentials (if required):

use admin
db.auth("<username>", "<password>")
List databases:

show dbs
Switch to your database:

use <your_database>
Insert a test document:

javascript

db.<collection_name>.insertOne({ name: "Sample Item", value: 123 });
Verify the inserted data:

javascript
Copy code
db.<collection_name>.find();

Option B: Use MongoDB Compass
Download and install MongoDB Compass on your machine.

Connect to MongoDB using the connection string:
mongodb://<username>:<password>@localhost:27017/<database_name>
Browse the database and collections to insert/view data.

# 3. Use a Node.js Endpoint (if applicable)
If your Node.js app has endpoints for interacting with the database:

Check if the Node.js service is running:


docker ps
Test the API using a tool like curl or Postman. For example:

GET Data:

curl http://localhost:3000/items
POST Data:

curl -X POST -H "Content-Type: application/json" -d '{"name": "New Item", "value": 123}' http://localhost:3000/items
Verify the data was inserted by accessing the database via mongosh or MongoDB Compass.

# 4. Verify Data Persistence
To ensure the data persists after restarting the container:

Stop the containers:

docker-compose down
Start them again:

docker-compose up

Connect to MongoDB and verify the data is still present:
bash
Copy code
docker exec -it <container_id> mongosh
use <your_database>
db.<collection_name>.find();
Troubleshooting Tips
Connection Issues: Ensure your Node.js app or client connects to mongodb://mongodb:27017/ (service name in Docker Compose) if containers are on the same network.
Check Logs: Look at logs for MongoDB or Node.js for error messages:

docker logs <mongodb_container_id>
docker logs <nodejs_container_id>
Validate Network: Ensure both services are in the same Docker Compose network.
Let me know if you encounter any issues!
