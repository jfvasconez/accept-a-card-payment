
# Stripe Test App
The bulk of the code used here was acquired by running `stripe samples create accept-a-card-payment` via the Stripe CLI and selecting `using-webhooks`, `web`, and `node` when prompted. I have made a few cosmetic changes to make it my own and also to log successful purchases in a separate file.

To avoid confusion, I have renamed the 2 readMe files that were originally provided by Stripe to `Stripe - Original README.md`. You do not need to read these unless you're curious, since my ReadMe covers the steps you'll need to take to run it.

# Prerequisites
1. Stripe CLI. 

        https://stripe.com/docs/stripe-cli
2. Node v10+. 

        https://nodejs.org/en/download/

# Instructions
1. You'll need a new file called `.env` file within `accept-a-card-payment/server`. To make things easy, I've provided a sample file called `sample_env.txt` in `accept-a-card-payment/server` that you can use. Open it now to get started.
    
    You can get your `STRIPE_WEBHOOK_SECRET` by running `stripe listen` in a new terminal window. (Note: You can run this from any directory). You can close this terminal window when you're done getting your key.
    
    Your `STRIPE_PUBLISHABLE_KEY` and `STRIPE_SECRET_KEY` can be found at https://dashboard.stripe.com/test/apikeys. 
    
    If you were making your changes within `sample_env.txt`, rename it `.env` when you're done.
    
    Optional: `STATIC_DIR` can be left unchanged unless you move files around within the sample code. 
2. Open a new terminal window and navigate to `accept-a-card-payment/server`. Run `npm install` followed by `npm start`. Leave it running.
3. In a new terminal window, run `stripe listen --forward-to localhost:4242/webhook`. This can be from any directory. Leave it running.
4. In your browser, go to: `http://localhost:4242/`
5. Try a purchase using the card `4242424242424242` with any zip code, expr date, and cvc code. It should succeed.
6. Try a purchase using the card `4000002500003155` with any zip code, expr date, and cvc code. Click on "Complete Authentication" in the authentication prompt. It should succeed when you accept. 
7. Try a purchase using the card `4000000000009995` with any zip code, expr date, and cvc code. It should fail due to insufficient funds.
8. You can verify these tests worked by going to `https://stripe.com/docs/payments/accept-a-payment#web-test-integration` and clicking on the button `Check Payments`.
9. Successful purchases will be recorded in a file called `Fulfillment.log` located within `accept-a-card-payment/server`.
       
    Note: If purchases are not being recorded in the file, there may be a write permission issue on your machine.