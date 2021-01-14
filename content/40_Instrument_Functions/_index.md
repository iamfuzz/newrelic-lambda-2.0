+++
title = "Instrument Lambda Functions"
chapter = false
weight = 40
+++

## Instrumenting AWS Lambda Functions

Now that we have linked your AWS and New Relic accounts, let's install the New Relic Lambda layer for each of the AWS Lambda functions we wish to monitor in our AWS Bookstore application.

Copy the commands listed below, one at a time, into CloudShell to instrument your Lambda functions (You will need to replace YOUR_NR_ACCOUNT_ID with your actual New Relic account ID that you stored earlier in a text file):

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-ListOrdersInCart --upgrade

```

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-AddToCart --upgrade
```

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-ListOrders --upgrade
```

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-GetCartItem --upgrade
```

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-Checkout --upgrade
```

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-UpdateCart --upgrade
```

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-GetBook --upgrade
```

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-RemoveFromCart --upgrade
```

```bash
newrelic-lambda layers install --nr-account-id YOUR_NR_ACCOUNT_ID --function mybookstore-ListBooks --upgrade
```

All future layers versions will include the Lambda extension by default.

To list your Lambda functions and verify that they are now instrumented, you can run the following command:

```bash
newrelic-lambda layers list
```

Congratulations!  You have successfully instrumented the Lambda functions for your AWS Bookstore application!
