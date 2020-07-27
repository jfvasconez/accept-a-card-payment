
# Stripe Test App
The bulk of the code used here was acquired by running `stripe samples create accept-a-card-payment` via the Stripe CLI and selecting `using-webhooks` and `node` when prompted.

To avoid confusion, I have renamed the 2 readMe files that were provided to `Stripe - Original README.md` 

# Prerequisites
1. Stripe CLI. 

        https://stripe.com/docs/stripe-cli
2. Node v10+. 

        https://nodejs.org/en/download/

# INSTRUCTIONS
1. In your terminal, run `stripe listen --forward-to localhost:4242/webhook`. This can be run from any directory. Copy the webhook signing secret, you'll need it in the next step. You'll also want to keep this running in terminal as you go through the next steps so don't close it.
2. You'll need a new file called `.env` file within `accept-a-card-payment/server`. To make things easy, I've provided a sample file called `sample_env.txt` in `accept-a-card-payment/server` that you can use. Open it now to get started.
    Step 1: Paste the "webhook signing secret" from step 1 into the field titled `STRIPE_WEBHOOK_SECRET`.
    Step 2: Your `STRIPE_PUBLISHABLE_KEY` and `STRIPE_SECRET_KEY` can be found at https://dashboard.stripe.com/test/apikeys. 
    Step 3: Rename the file to `.env` when you're done.
    Optional: `STATIC_DIR` can be left unchanged unless you move files around within the sample code. 
3. Open a new terminal window and navigate to `accept-a-card-payment/server`. Run `npm install`
4. Still within `accept-a-card-payment/server`, run `npm start`
5. In your browser, go to: `http://localhost:4242/`
6. Try a purchase using the card `4242424242424242` with any zip code, expr date, and cvc code. It should succeed.
7. Try a purchase using the card `4000002500003155` with any zip code, expr date, and cvc code. Click on "Complete Authentication" in the authentication prompt. It should succeed when you accept. 
8. Try a purchase using the card `4000000000009995` with any zip code, expr date, and cvc code. It should fail due to insufficient funds.
9. You can verify these tests worked by going to `https://stripe.com/docs/payments/accept-a-payment#web-test-integration` and clicking on the button `Check Payments`.
10. Successful purchases will be recorded in a file called `Fulfillment.log` located within `accept-a-card-payment/server`.
       
    Note: If purchases are not being recorded in the file, there may be a write permission issue on your machine.

# Extra
1. You may need the node package  “simple-node-logger” to record to fulfillment.log
        
        In your terminal, navigate to `accept-a-card-payment/server` and run `npm install simple-node-logger --save`.
       
        More info at: https://www.npmjs.com/package/simple-node-logger.