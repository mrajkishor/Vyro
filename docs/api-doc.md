### RESTful API Documentation for Vehicle Rental Application (MVP v1)

#### Base URL
`https://api.vyro.com/v1`

#### Authentication
- **POST `/auth/requestOtp`**
  - Description: Request an OTP for a given mobile phone number.
  - Request Body:
    - `phoneNumber`: string (in international format, e.g., +1234567890)
  - Response:
    - `message`: string (e.g., "OTP sent successfully.")
    - `sessionId`: string (optional, for tracking the OTP session)

- **POST `/auth/verifyOtp`**
  - Description: Verify the OTP entered by the user.
  - Request Body:
    - `phoneNumber`: string
    - `otp`: string
    - `sessionId`: string (optional, received from `/auth/requestOtp`)
  - Response:
    - `token`: string (authentication token)
    - `userType`: string (`buyer` or `seller`)
    - `isNewUser`: boolean (indicates if it's a new user registration or an existing user)

#### User Registration (Post-Verification)
- **POST `/users/register`**
  - Description: Register a new user after OTP verification.
  - Request Body:
    - `phoneNumber`: string
    - `userType`: string (`buyer` or `seller`)
    - Additional user details (e.g., `name`, `location`, etc.)
  - Response:
    - `userId`: string
    - `message`: string

#### User Login (Post-Verification)
- **POST `/users/login`**
  - Description: Log in an existing user after OTP verification.
  - Request Body:
    - `phoneNumber`: string
  - Response:
    - `userId`: string
    - `userType`: string
    - `token`: string (authentication token)

### Notes on the Authentication Flow
- **Two-Step Verification**: The process involves two main steps: requesting an OTP and verifying it.
- **Session Handling**: Optionally, a `sessionId` can be used to securely link the OTP request and verification.
- **User Registration and Login**: After OTP verification, additional endpoints handle new user registration and existing user login. This separation allows for different handling of new versus returning users.
- **Security Considerations**: Ensure secure transmission of phone numbers and OTPs. Consider implementing rate limiting and other security measures to prevent abuse of the OTP mechanism.

#### Buyer's App APIs
- **GET `/vehicles/search`**
  - Description: Search for vehicles based on filters.
  - Query Parameters:
    - `location`: string
    - `type`: string
    - `dateRange`: string
  - Response:
    - List of vehicles with details.

- **GET `/vehicles/details/{vehicleId}`**
  - Description: Get detailed information about a specific vehicle.
  - Path Parameters:
    - `vehicleId`: string
  - Response:
    - Vehicle details including availability.

- **POST `/bookings/create`**
  - Description: Create a new booking.
  - Request Body:
    - `vehicleId`: string
    - `userId`: string
    - `startDate`: string
    - `endDate`: string
  - Response:
    - `bookingId`: string
    - `status`: string

- **POST `/payments/process`**
  - Description: Process payment for a booking.
  - Request Body:
    - `bookingId`: string
    - `paymentDetails`: object
  - Response:
    - `paymentId`: string
    - `status`: string

- **GET `/users/tripHistory/{userId}`**
  - Description: Retrieve trip history for a user.
  - Path Parameters:
    - `userId`: string
  - Response:
    - List of past trips and ratings.

#### Seller's App APIs
- **POST `/vehicles/add`**
  - Description: Add a new vehicle listing.
  - Request Body:
    - `sellerId`: string
    - `vehicleDetails`: object
  - Response:
    - `vehicleId`: string
    - `message`: string

- **GET `/bookings/manage/{sellerId}`**
  - Description: Get bookings for the seller's vehicles.
  - Path Parameters:
    - `sellerId`: string
  - Response:
    - List of bookings with status.

- **GET `/payments/earnings/{sellerId}`**
  - Description: Retrieve earnings and payment details for a seller.
  - Path Parameters:
    - `sellerId`: string
  - Response:
    - Earnings and transaction details.

- **GET `/analytics/shopPerformance/{sellerId}`**
  - Description: Get shop performance analytics.
  - Path Parameters:
    - `sellerId`: string
  - Response:
    - Analytics data and performance graphs.

#### Common Endpoints
- **POST `/feedback/rate`**
  - Description: Submit a rating for a trip or vehicle.
  - Request Body:
    - `userId`: string
    - `vehicleId`: string
    - `rating`: integer
    - `comments`: string (optional)
  - Response:
    - `message`: string

#### Error Handling
Each endpoint includes standard HTTP status codes for success (e.g., 200, 201) and error responses (e.g., 400, 401, 500), along with a message describing the error in the response body.

#### Security
Ensuring secure communication by using HTTPS and authenticating requests using the provided token in the Authorization header.

---
### Further Optimisation with GraphQL 
In the above API documentation, several endpoints could benefit from being implemented with GraphQL instead of REST, especially those involving complex data structures or requiring flexibility in the data retrieved. Hence breaking down of APIs which could be effectively replaced by GraphQL:

### APIs Suitable for GraphQL

1. **Vehicle Search and Filtering (Buyer's App)**
   - REST Endpoint: `GET /vehicles/search`
   - GraphQL Advantage: Allows buyers to specify exactly which attributes of the vehicles they're interested in (e.g., make, model, price, location, availability) in a single query, reducing over-fetching.

2. **Vehicle Details and Availability (Buyer's App)**
   - REST Endpoint: `GET /vehicles/details/{vehicleId}`
   - GraphQL Advantage: Can efficiently fetch detailed information about a vehicle, including nested data like owner details, ratings, and reviews, in one request.

3. **Trip History and Ratings (Buyer's App)**
   - REST Endpoint: `GET /users/tripHistory/{userId}`
   - GraphQL Advantage: Users can query their trip history and related details (like vehicle used, duration, ratings given) in a single request, with the flexibility to retrieve only the needed data.

4. **Managing Bookings and Availability (Seller's App)**
   - REST Endpoint: `GET /bookings/manage/{sellerId}`
   - GraphQL Advantage: Sellers can query bookings, vehicle details, and availability in one go, and can dynamically adjust the query to fit the data they need at the moment.

5. **Shop Management and Analytics (Seller's App)**
   - REST Endpoint: `GET /analytics/shopPerformance/{sellerId}`
   - GraphQL Advantage: Complex data like analytics and performance metrics can be tailored in a single query, allowing sellers to fetch specific insights without redundant data.

6. **Vehicle Listing and Details (Seller's App)**
   - REST Endpoint: `POST /vehicles/add`
   - GraphQL Advantage: While adding vehicles, sellers might want to immediately query related data (like predicted earnings or comparison with other vehicles) which can be efficiently handled in GraphQL.

### General Considerations for GraphQL
- **Single Unified Endpoint**: GraphQL uses a single endpoint to handle all queries and mutations, making it easier to manage than multiple REST endpoints.
- **Complex Queries and Mutations**: For operations that involve multiple steps in REST (like creating a booking and then processing a payment), GraphQL can handle this more efficiently in a single mutation.
- **Real-Time Data with Subscriptions**:  When the application requires real-time updates (e.g., vehicle availability changes), GraphQL subscriptions are beneficial.

### So,
Moving to GraphQL for these aspects of this application could enhance flexibility, reduce unnecessary data transfer, and simplify the interaction between the frontend and backend. 
