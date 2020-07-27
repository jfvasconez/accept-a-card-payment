
# Stripe Test App
The bulk of the code used here was acquired by running `stripe samples create accept-a-card-payment` via the Stripe CLI and selecting `using-webhooks` and `node` when prompted.

To avoid confusion, I have renamed the 2 readMe files that were provided to `Stripe - Original README.md` 

# Prerequisites
1. Stripe CLI. 

        https://stripe.com/docs/stripe-cli
2. Node v10+. 

        https://nodejs.org/en/download/

# INSTRUCTIONS
1. Create a file called `.env` file within `accept-a-card-payment/server`.

    There is a file called `sample_env.txt` in `accept-a-card-payment/server` that you can use as a guide. You simply need to fill in your `STATIC_DIR` (I used "../client"), `STRIPE_PUBLISHABLE_KEY`, `STRIPE_SECRET_KEY`, and `STRIPE_WEBHOOK_SECRET` and rename the file to `.env` when you're done.
    
    Your API keys can be found at: https://dashboard.stripe.com/test/apikeys. Note: If you have already setup the CLI, your `STRIPE_WEBHOOK_SECRET` will be found under the section "Restricted Keys" within a row called "CLI Key for [machine]"
2. Navigate to `accept-a-card-payment/server` in terminal and run `npm install`
3. Run `npm start`
4. In a new terminal, run `stripe listen --forward-to localhost:4242/webhook`
5. In your browser, go to: `http://localhost:4242/`
6. Try a purchase using the card `4242424242424242` with any zip code, expr date, and cvc code. It should succeed.
7. Try a purchase using the card `4000002500003155` with any zip code, expr date, and cvc code. Click on "Complete Authentication" in the authentication prompt. It should succeed when you accept. 
8. Try a purchase using the card `4000000000009995` with any zip code, expr date, and cvc code. It should fail due to insufficient funds.
9. You can verify these tests worked by going to `https://stripe.com/docs/payments/accept-a-payment#web-test-integration` and clicking on the button `Check Payments`.
9. Successful purchases will be recorded in a file called `Fulfillment.log` located within `accept-a-card-payment/server`.
       
    Note: If purchases are not being recorded in the file, there may be a write permission issue on your machine.

# Extra
1. You may need the node package  “simple-node-logger”.
        
        You should install at `accept-a-card-payment/server` with `npm install simple-node-logger --save`.
       
        More info at: https://www.npmjs.com/package/simple-node-logger.