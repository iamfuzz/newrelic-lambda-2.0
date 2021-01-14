+++
title = "Enable Serverless Monitoring"
chapter = false
weight = 30
+++

{{% notice note %}}
To continue this workshop, a New Relic account is required.  A new account is recommended and can be created by clicking [here](https://newrelic.com/signup)
{{% /notice %}}

## Serverless Monitoring for AWS Lambda

Serverless monitoring for AWS Lambda offers in-depth performance monitoring for your Lambda functions. When you enable serverless monitoring using our Lambda extension, this is what happens:

![Monitoring Diagram](/images/enable_monitoring/lambda-monitoring.png)

 1. You configure your Lambda function to include our layer for the runtime you've chosen.
 1. As your code runs, our Lambda layer gathers telemetry data about the invocation and its execution.
 1. Just before execution finishes, the Lambda layer sends the data it has gathered to the New Relic Lambda extension, which is bundled with the layer.
 1. The extension sends the data to New Relic, along with additional information from AWS Lambda.

### What's in the New Relic Lambda layer?
The layer for your runtime contains the New Relic Lambda extension  . This executable extends your Lambda function. The extension sends telemetry data to New Relic, and interacts with AWS directly to enhance the data we gather, while minimizing the impact of instrumentation on your application's performance.

For Node.js and Python, the layer contains the New Relic agent code, and a wrapper for your Lambda handler. For other runtimes, we take an SDK approach, providing you with the tools to instrument your code, while taking advantage of emerging standards like OpenTracing and OpenTelemetry.

### Enable serverless monitoring
Two things have to happen to let New Relic gather telemetry from your Lambda functions.

 1. Link your AWS account with your New Relic account.
 1. Configure each of your functions to include our Lambda extension.

In this section we will be linking your AWS account with your New Relic account.

### Link your AWS account with your New Relic account
When you link your AWS account to New Relic, you're granting permission to New Relic to create an inventory of your AWS account, and gather CloudWatch metrics for your Lambda functions. Resources in your AWS account then show up as entities in the entity explorer, decorated with config information.

**To link your account, you will need the following information:**

 * Your New Relic account ID.
 * Your New Relic personal User key

### Finding your New Relic account ID

You can locate this by visiting your [New Relic One homepage](https://one.newrelic.com/), logging in, clicking on the button at the top right hand corner of the screen, and selecting ***Account settings***:
 
![Account Settings](/images/enable_monitoring/account-settings.png)

On the Account settings page you will see your account name and number presented in a dropdown box near the top of the page:

![Account ID](/images/enable_monitoring/account-id.png)

Open your favorite text editor and type in your New Relic account ID so that you can easily copy and paste it later.

### Create a New Relic User key

Navigate to your [New Relic One homepage](https://one.newrelic.com/) and once again click on the button at the top right hand corner of the screen.  This time, select ***API keys*** from the dropdown dialog:

![API Keys](/images/enable_monitoring/api-keys.png)

On the API keys page, click on the ***Create key*** button located toward the right hand side of your screen:

![Create key](/images/enable_monitoring/create-key.png)

Create your key by filling out the form on the right hand side of your screen as shown below, ensuring that the **Key type** field is set to **User**, and clicking on the ***Create key*** button:

![Create key dialog](/images/enable_monitoring/create-key-dialog.png)

Copy your newly created key (as shown below) and paste it in the text file you created earlier to store your New Relic account ID:

![Copy key](/images/enable_monitoring/copy-key.png)

### Open CloudShell

AWS CloudShell is a browser-based shell that makes it easy to securely manage, explore, and interact with your AWS resources. CloudShell is pre-authenticated with your console credentials. Common development and operations tools are pre-installed, so no local installation or configuration is required. With CloudShell, you can quickly run scripts with the AWS Command Line Interface (AWS CLI), experiment with AWS service APIs using the AWS SDKs, or use a range of other tools to be productive. You can use CloudShell right from your browser and at no additional cost.

Locate and open CloudShell using the search bar in the AWS Console:

![CloudShell](/images/enable_monitoring/open-cloudshell.png)

Within CloudShell, install the New Relic CLI tool by executing the following command:

```bash
pip3 install newrelic-lambda-cli --user
```

Now that the New Relic CLI tool is installed, we can link our accounts by executing the following command (YOUR_LINKED_ACCOUNT_NAME refers to your New Relic account and can be named anything you wish):

```bash
newrelic-lambda integrations install --nr-account-id YOUR_NR_ACCOUNT_ID --linked-account-name YOUR_LINKED_ACCOUNT_NAME --nr-api-key YOUR_NEW_RELIC_USER_KEY
```

If successful, you should see output similar to:

```
Validating New Relic credentials
Retrieving integration license key
Checking for a pre-existing link between New Relic and AWS
Creating the AWS role for the New Relic AWS Lambda Integration
Waiting for stack creation to complete... ✔ Done
...
✨ Install Complete ✨
```

Congratulations!  You have successfully linked your AWS account with New Relic!  

### Multiple AWS regions and accounts in a real-world environment

The newrelic-lambda CLI should be run once per region, with the --aws-region parameter. Use the same linked account name, and the tool will detect that the account link has been created already. The license key secret needs to be created in each region.

Similarly, several AWS accounts can be linked to a New Relic account. Give each account a different linked account name. The --aws-profile argument to the CLI tool will select the named profile. The tool uses the same configuration as the AWS CLI.

### Cleanup

If you no longer wish for your AWS account to be connected to New Relic, simply access CloudFormation from the AWS Console and dleete any stacks that begin with NewRelic.
