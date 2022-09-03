<!-- @format -->

To run this web service, procedure is outlined below:

Ensure Node.js is downloaded on machine
Clone the repository onto your machine
Check the following dev dependencies packages are installed: npm i express express-async-handler
Check start and server scripts are present in package.json and initialize "npm run server" to boot up the project on localhost:8000 || localhost:3000

Rules:

1. We want the oldest points to be spent first (oldest based on transaction timestamp, not the order they’re received)
2. We want no payer's points to go negative.

Web service uses the same HTTP query as there was no requirement to get a specific payer data and below outlines the HTTP request (Done on Postman):

1. A POST request sent to api/rewards
   Parameters: An object with three required fields (payer, points, date).
   The payer field contains the string type for name of an institution or company in the example. The points field contains the number value for the points recorded from the transaction. The supplied timestamp for the date of transaction and inserted into the object.
   Response: Add transactions object containing a specific payer, point amount and date onto pointTransaction array.

2. A PUT request sent to api/rewards
   Parameters: Spend points using the rules above and return a list of { "payer": <string>, "points": <integer> } for each call stored in "pointsTransaction".
   Response: returns the updated "payerSummaryBalance" object.

3. A GET request sent to /api/v1/payers/balances
   Parameters: transaction array must has data to proceed.
   Response: An object "containing the key of the payer as well as their remaining points balance.

## How to test

- run `npm i` to install all dependencies if not done yet
- run `npm test` to run test cases

I have the following test cases written:

- Invalid input
  - Send a request to a wrong api
  - Send a transaction with only two keys
  - Spend more points than available
- ## Valid input
  - Send 1 Transaction
  - Send 2nd Transaction
  - Spend valid amount
  - Get current balance
- Following the example from backend assignment
  - adding multiple transactions
  - spending 5000 points
  - get balance call results
