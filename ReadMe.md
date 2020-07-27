
# Stripe Test App
The bulk of the code used here was acquired  via `stripe samples create accept-a-card-payment` using the `web` and `node` options in the prompt.

To avoid confusion, I have renamed the 2 readMe files that were provided to `Stripe - Original README.md` 

# MAKE SURE YOU HAVE THE FOLLOWING INSTALLED ON YOUR MACHINE
1. Stripe CLI. 

        https://stripe.com/docs/stripe-cli
2. Node v10+. 

        https://nodejs.org/en/download/

# INSTRUCTIONS
1. Create a file called `.env` file within `accept-a-card-payment/server`.

    There is a file called `.env.example` in the root directory `accept-a-card-payment` that you can use as a guide. You simply need to fill in your `STATIC_DIR` (I used "../client"), `STRIPE_PUBLISHABLE_KEY`, `STRIPE_SECRET_KEY`, and `STRIPE_WEBHOOK_SECRET`. They can be found at: https://dashboard.stripe.com/test/apikeys.
    
    Pro-tip, if you install the sample app using `stripe samples create accept-a-card-payment`, and select `webhook` and `node` when prompted, you'll automatically get a `.env` created for you using your personal keys that you can use in my test app. (note: The secret key was wrong for me when I did that, so I had to update it myself manually)
2. Navigate to `accept-a-card-payment/server` in terminal and run `npm install`
3. Run `npm start`
4. In a new terminal window or tab, run `stripe listen --forward-to localhost:4242/webhook`
5. In your browser, go to: `http://localhost:4242/`
6. Try a purchase using the card `4242424242424242` with any zip code, expr date, and cvc code. It should succeed.
7. Try a purchase using the card `4000002500003155` with any zip code, expr date, and cvc code. You should receive an authentication prompt. It should succeed when you accept. 
8. Try a purchase using the card `4000000000009995` with any zip code, expr date, and cvc code. It should fail due to insufficient funds.
9. Successful purchases will be recorded in a file called `Fullfillment.log` located within `accept-a-card-payment/server`.
       
        Note: If purchases are not being recorded in the file, there may be a write permission issue on your machine.

# Extra
1. You may need the node package  “simple-node-logger”.
        
        You should install at `accept-a-card-payment/server` with `npm install simple-node-logger --save`.
       
        More info at: https://www.npmjs.com/package/simple-node-logger.