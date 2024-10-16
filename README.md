# AirlineMicroservices

A collection of microservices for managing airline operations, including airlines, flights, and passengers. This project demonstrates inter-service communication and RESTful API design using Node.js and MongoDB.

## Folder Structure

```
AirlineMicroservices/
├── airline-company-microservice/
├── flight-microservice/
└── passenger-microservice/
```

## Endpoints

### Airline Company Microservice

#### 1. **Create a New Airline**
- **POST** `/airlines`
- **Request Body:**
  ```json
  {
    "airlineName": "Air India",
    "hq": "New Delhi"
  }
  ```

#### 2. **Get All Airlines**
- **GET** `/airlines`
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

#### 3. **Get Airline by ID**
- **GET** `/airlines/:id`
- **Response:**
  ```json
  {
    "_id": "60d5f4c3e65c1b3e68c81e57",
    "airlineName": "Air India",
    "hq": "New Delhi"
  }
  ```

#### 4. **Get All Flights under an Airline**
- **GET** `/airlines/:id/flights`
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

---

### Flight Microservice

#### 1. **Create a New Flight**
- **POST** `/flights`
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

#### 2. **Get All Flights**
- **GET** `/flights`
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

#### 3. **Get Flight by ID**
- **GET** `/flights/:id`
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

#### 4. **Get All Passengers under a Flight**
- **GET** `/flights/:id/passengers`
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

---

### Passenger Microservice

#### 1. **Create a New Passenger**
- **POST** `/passengers`
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

#### 2. **Get All Passengers**
- **GET** `/passengers`
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

#### 3. **Get Passenger by ID**
- **GET** `/passengers/:id`
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

---

## Getting Started

1. **Clone the repository**:
   ```bash
   git clone https://github.com/MuhammedBasith/AirlineMicroservices.git
   cd AirlineMicroservices
   ```

2. **Install dependencies**:
   - For each microservice, navigate to the respective folder and run:
     ```bash
     npm install
     ```

3. **Run the microservices**:
   - Start each microservice in separate terminal windows:
     ```bash
     node airline-company-microservice/index.js
     node flight-microservice/index.js
     node passenger-microservice/index.js
     ```

4. **Test the APIs**: Use a tool like Postman or curl to test the endpoints.

---

## License
This project is licensed under the MIT License.
