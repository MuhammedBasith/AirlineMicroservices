# AirlineMicroservices
A collection of microservices for managing airline operations, including airlines, flights, and passengers. This project demonstrates inter-service communication and RESTful API design using Node.js and MongoDB.

## Folder Structure
```
AirlineMicroservices/
├── airline-company-microservice/
├── flight-microservice/
├── passenger-microservice/
├── api-gateway/
└── docker-compose.yml
```

## Endpoints

### Airline Company Microservice
1. **Create a New Airline**
   - **POST /airlines**
   - **Request Body:**
     ```json
     {
       "airlineName": "Air India",
       "hq": "New Delhi"
     }
     ```
  
2. **Get All Airlines**
   - **GET /airlines**
   - **Response:**
     ```json
     [
       {
         "_id": "60d5f4c3e65c1b3e68c81e57",
         "airlineName": "Air India",
         "hq": "New Delhi"
       },
       {
         "_id": "60d5f4c3e65c1b3e68c81e58",
         "airlineName": "Delta Airlines",
         "hq": "Atlanta"
       }
     ]
     ```

3. **Get Airline by ID**
   - **GET /airlines/:id**
   - **Response:**
     ```json
     {
       "_id": "60d5f4c3e65c1b3e68c81e57",
       "airlineName": "Air India",
       "hq": "New Delhi"
     }
     ```

4. **Get All Flights under an Airline**
   - **GET /airlines/:id/flights**
   - **Response:**
     ```json
     [
       {
         "_id": "60d5f4c3e65c1b3e68c81e59",
         "flightNumber": "AI 101",
         "airlineId": "60d5f4c3e65c1b3e68c81e57",
         "departureAirport": "DEL",
         "arrivalAirport": "BOM",
         "duration": "2h 30m",
         "totalSeats": 180
       }
     ]
     ```

### Flight Microservice
1. **Create a New Flight**
   - **POST /flights**
   - **Request Body:**
     ```json
     {
       "flightNumber": "AI 101",
       "airlineId": "60d5f4c3e65c1b3e68c81e57",
       "departureAirport": "DEL",
       "arrivalAirport": "BOM",
       "duration": "2h 30m",
       "totalSeats": 180
     }
     ```

2. **Get All Flights**
   - **GET /flights**
   - **Response:**
     ```json
     [
       {
         "_id": "60d5f4c3e65c1b3e68c81e59",
         "flightNumber": "AI 101",
         "airlineId": "60d5f4c3e65c1b3e68c81e57",
         "departureAirport": "DEL",
         "arrivalAirport": "BOM",
         "duration": "2h 30m",
         "totalSeats": 180
       }
     ]
     ```

3. **Get Flight by ID**
   - **GET /flights/:id**
   - **Response:**
     ```json
     {
       "_id": "60d5f4c3e65c1b3e68c81e59",
       "flightNumber": "AI 101",
       "airlineId": "60d5f4c3e65c1b3e68c81e57",
       "departureAirport": "DEL",
       "arrivalAirport": "BOM",
       "duration": "2h 30m",
       "totalSeats": 180
     }
     ```

4. **Get All Passengers under a Flight**
   - **GET /flights/:id/passengers**
   - **Response:**
     ```json
     [
       {
         "_id": "60d5f4c3e65c1b3e68c81e60",
         "name": "John Doe",
         "gender": "Male",
         "nationality": "Indian",
         "contactInfo": {
           "email": "john.doe@example.com",
           "phone": "1234567890"
         },
         "flightId": "60d5f4c3e65c1b3e68c81e59"
       }
     ]
     ```

### Passenger Microservice
1. **Create a New Passenger**
   - **POST /passengers**
   - **Request Body:**
     ```json
     {
       "name": "John Doe",
       "gender": "Male",
       "nationality": "Indian",
       "contactInfo": {
         "email": "john.doe@example.com",
         "phone": "1234567890"
       },
       "flightId": "60d5f4c3e65c1b3e68c81e59"
     }
     ```

2. **Get All Passengers**
   - **GET /passengers**
   - **Response:**
     ```json
     [
       {
         "_id": "60d5f4c3e65c1b3e68c81e60",
         "name": "John Doe",
         "gender": "Male",
         "nationality": "Indian",
         "contactInfo": {
           "email": "john.doe@example.com",
           "phone": "1234567890"
         },
         "flightId": "60d5f4c3e65c1b3e68c81e59"
       }
     ]
     ```

3. **Get Passenger by ID**
   - **GET /passengers/:id**
   - **Response:**
     ```json
     {
       "_id": "60d5f4c3e65c1b3e68c81e60",
       "name": "John Doe",
       "gender": "Male",
       "nationality": "Indian",
       "contactInfo": {
         "email": "john.doe@example.com",
         "phone": "1234567890"
       },
       "flightId": "60d5f4c3e65c1b3e68c81e59"
     }
     ```

## Getting Started

### Clone the Repository:
```bash
git clone https://github.com/MuhammedBasith/AirlineMicroservices.git
cd AirlineMicroservices
```

### Install Dependencies:
For each microservice, navigate to the respective folder and run:
```bash
npm install
```

### Running with Docker and Docker Compose

This project can also be run using Docker and Docker Compose, which simplifies the setup and management of services.

#### 1. Docker Setup

Each microservice and the API gateway can be containerized using Docker. Here’s how to do it:

- **Dockerfile for Each Microservice**: Each microservice should have a `Dockerfile` that specifies how to build the Docker image.

- **API Gateway Dockerfile**: Similarly, create a Dockerfile for the API gateway.

#### 2. Docker Compose Configuration

You can use Docker Compose to run all services together. The following `docker-compose.yml` configuration includes MongoDB as well:

```yaml
version: '3.8'

services:
  api-gateway:
    build:
      context: ./api-gateway
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    depends_on:
      - airline-company-microservice
      - flight-microservice
      - passenger-microservice

  airline-company-microservice:
    build:
      context: ./airline-company-microservice
      dockerfile: Dockerfile
    ports:
      - "3001:3001"
    environment:
      - MONGODB_URI=mongodb://mongo:27017/airlineDB
    depends_on:
      - mongo

  flight-microservice:
    build:
      context: ./flight-microservice
      dockerfile: Dockerfile
    ports:
      - "3002:3002"
    environment:
      - MONGODB_URI=mongodb://mongo:27017/flightDB
    depends_on:
      - mongo

  passenger-microservice:
    build:
      context: ./passenger-microservice
      dockerfile: Dockerfile
    ports:
      - "3003:3003"
    environment:
      - MONGODB_URI=mongodb://mongo:27017/passengerDB
    depends_on:
      - mongo

  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

#### 3. Build and Run the Containers
To build and run your containers with the updated configuration, use:
```bash
docker-compose up --build
```

### Testing the APIs
Once the services are running, use a tool like Postman or curl to test the endpoints via the API gateway.

## License
This project is licensed under the MIT License.
