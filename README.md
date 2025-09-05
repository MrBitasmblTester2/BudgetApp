# BudgetApp

Description
A platform that helps users manage expenses, set savings goals, and receive AI-powered recommendations for smarter financial decisions.

## Tech Stack
- Go (API & Back-End)
- Express.js (API & Back-End)
- ASP.NET Core (API & Back-End)

## Requirements
- Transaction categorization system (support custom and auto-categorized transactions)
- Budget tracking with goal progress (recalculate after each transaction)
- AI-powered spending insights (start with static rules before integrating AI models)

## Installation

### Prerequisites
- Go 1.18+ installed
- Node.js 14+ and npm installed
- .NET 6 SDK installed
- A running database instance (PostgreSQL, MySQL, or MongoDB)

### Environment Variables
Create a `.env` file in each service directory with:

DATABASE_URL=<your_database_connection_string>
OPENAI_API_KEY=<your_openai_api_key>
JWT_SECRET=<your_jwt_secret>


### Go Service Setup
bash
cd go-service
go mod tidy
go run main.go


### Express.js Service Setup
bash
cd express-service
npm install
npm run build
npm start


### ASP.NET Core Service Setup
bash
cd aspnet-service
dotnet restore
dotnet run --project BudgetApp.Api/BudgetApp.Api.csproj


## Usage
After all services are running, you can interact via HTTP clients like curl or Postman. Example:
bash
# Create a transaction
curl -X POST http://localhost:8080/transactions \
  -H "Content-Type: application/json" \
  -d '{"amount": 50, "description": "Groceries", "date": "2024-06-01"}'

# Check budget progress
curl http://localhost:8080/budgets/1/progress

# Get spending insights
curl http://localhost:8080/insights


## Implementation Steps
1. Scaffold three back-end services:
   - Go for core transaction and categorization API
   - Express.js for budget tracking and goal management
   - ASP.NET Core for AI insights and rules engine placeholder
2. Define data models for users, transactions, categories, and budgets.
3. Implement transaction endpoints with custom and auto-categorization logic in Go.
4. Build budget endpoints in Express.js, recalculate goal progress on each transaction event.
5. Create a static rules engine in ASP.NET Core to generate initial spending insights.
6. Connect all services to the shared database and wire up environment variables.
7. Write unit and integration tests for each service.
8. Prepare for AI integration by designing a pluggable module in ASP.NET Core.

## API Endpoints

### Transactions (Go Service)
- POST /transactions       Create or auto-categorize a transaction
- GET  /transactions       List all transactions

### Budgets (Express.js Service)
- POST /budgets            Create a new budget goal
- GET  /budgets/:id        Fetch budget details and progress

### Insights (ASP.NET Core Service)
- GET /insights            Retrieve static spending recommendations