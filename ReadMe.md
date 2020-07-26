
# Juan Vasconez - Stripe PM Take Home Assignment
The bulk of the code used here was acquired  via `stripe samples create accept-a-card-payment` using the `web` and `node` options in the prompt.

To avoid confusion, I have renamed the 2 readMe files that were provided to `Stripe - Original README.md` 

# MAKE SURE YOU HAVE THE FOLLOWING INSTALLED ON YOUR MACHINE
1. Stripe CLI
        https://stripe.com/docs/stripe-cli
2. Node
        https://nodejs.org/en/download/

# INSTRUCTIONS
1. Navigate to `accept-a-card-payment/server` in terminal and run `npm install`
2. Run `npm start`
3. In a new terminal window or tab, run `stripe listen --forward-to localhost:4242/webhook`
4. In your browser, go to: `http://localhost:4242/`
5. Try a purchase using the card `4242424242424242` with any zip code, expr date, and cvc code. It should succeed.
6. Try a purchase using the card `4000002500003155` with any zip code, expr date, and cvc code. You should receive an authentication prompt. It should succeed when you accept. 
7. Try a purchase using the card `4000000000009995` with any zip code, expr date, and cvc code. It should fail due to insufficient funds.
8. Successful purchases will be recorded in a file called `Fullfillment.log` located within `accept-a-card-payment/server`.
        Note: If purchases are not being recorded in the file, there may be a write permission issue on your machine.

# Extra
1. You may need the node package  “simple-node-logger”
        You should install at `accept-a-card-payment/server` with `npm install simple-node-logger --save`
        More info at: https://www.npmjs.com/package/simple-node-logger
