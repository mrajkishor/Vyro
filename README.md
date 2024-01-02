
# Vehicle Rental Application

Welcome to the Vehicle Rental Application! This mobile application connects users looking to rent vehicles with vehicle owners willing to rent out their vehicles. The application is divided into two main components: the Buyer's App and the Seller's App.

## Table of Contents

- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Contributing](#contributing)
- [License](#license)

## Getting Started

### Prerequisites

To run this project, you'll need to have the following installed on your local machine:

- Node.js
- npm or Yarn
- React Native CLI
- AWS CLI (for serverless deployment)

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/mrajkishor/Gyvor.git
   ```

2. Navigate to the project directory:

   ```bash
   cd Gyvor
   ```

3. Install dependencies:

   ```bash
   npm install
   ```

4. Set up your AWS credentials for serverless deployment:

   ```bash
   aws configure
   ```

   Follow the prompts to enter your AWS access key, secret key, region, and output format.

5. Run the application:

   ```bash
   npx react-native run-android
   ```

   or

   ```bash
   npx react-native run-ios
   ```

   Make sure you have an Android or iOS emulator set up.

## Project Structure

The project is structured as follows:

- `buyer-app/`: Source code for the Buyer's App.
- `seller-app/`: Source code for the Seller's App.
- `backend/`: AWS Lambda functions and serverless configuration.
- `docs/`: Documentation and design files.

## Tech Stack

- **Frontend:**
  - React Native
  - Redux or React Context API
  - Axios for API communication

- **Backend:**
  - AWS Lambda (Serverless)
  - API Gateway
  - AWS Cognito for user authentication

- **Database:**
  - Amazon DynamoDB

- **Storage:**
  - Amazon S3

## Contributing

Contributions are welcome! If you'd like to contribute to the project, please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and commit them.
4. Push your changes to your fork.
5. Submit a pull request.

Please make sure to follow the [code of conduct](CODE_OF_CONDUCT.md).

## License

This project is licensed under the [MIT License](LICENSE).