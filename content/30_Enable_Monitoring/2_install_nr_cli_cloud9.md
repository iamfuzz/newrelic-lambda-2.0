+++
title = "Enabling New Relic integrations using Cloud9"
chapter = false
weight = 2
+++


## Starting AWS Cloud9 IDE

{{% notice warning %}}
If you already installed the New Relic CLI with CloudShell, please skip this section.
{{% /notice %}}

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes pre-packaged with essential tools for popular programming languages and the AWS Command Line Interface (CLI) pre-installed so you don’t need to install files or configure your laptop for this workshop. 

Your Cloud9 environment will have access to the same AWS resources as the user with which you logged into the AWS Management Console. We strongly recommend using Cloud9 to complete this workshop.

**Cloud9 works best with Chrome or Firefox, not Safari. It cannot be used from a tablet.**

**:white_check_mark: Step-by-step Instructions**

1. From the AWS Management Console, Select **Services** then select **Cloud9** under Developer Tools. 

![Step 4](/images/getting_started/c9-step4.png)

2. Select **Create environment**.

3. Enter `wildrydes-webapp-development` into **Name** and optionally provide a **Description**.

![Step 5](/images/getting_started/c9-step5.png)

4. Select **Next step**.

5. In **Environment settings**:
- Set the *Instance type* to **t3.micro** by slecting the *Other instance type* radio button, then selecting ***t3.micro*** from the dropdown menu (shown below).
- Leave all other defaults unchanged.

![Step 6](/images/getting_started/c9-step6-b.png)

6. Select **Next step**.

7. Review the environment settings and select **Create environment**. It will take a couple of minutes for your Cloud9 environment to be provisioned and prepared.

## Setting up Cloud9 IDE

1. Once ready, your IDE will open to a welcome screen. Below that, you should see a terminal prompt. Close the Welcome tab and drag up the terminal window to give yourself more space to work in. 

![Step 7](/images/getting_started/c9-step7.png)

- You can run AWS CLI commands in here just like you would on your local computer. Remember for this workshop to run all commands within the Cloud9 terminal window rather than on your local computer.
- Keep your AWS Cloud9 IDE opened in a browser tab throughout this workshop.

2. Verify that your user is logged in by running the command `aws sts get-caller-identity`. Copy and paste the command into the Cloud9 terminal window. 

```console
aws sts get-caller-identity
```

- You'll see output indicating your account and user information:

```json
{
    "Account": "123456789012",
    "UserId": "AKIAIOSFODNN7EXAMPLE",
    "Arn": "arn:aws:iam::123456789012:user/Alice"
}
```
### :star: Tips

:bulb: Keep an open scratch pad in Cloud9 or a text editor on your local computer for notes. When the step-by-step directions tell you to note something such as an ID or Amazon Resource Name (ARN), copy and paste that into your scratch pad.

### :star: Recap

:key: This is your unique AWS account for this workshop. It will expire after you finish today.

:key: Use the same region for the entirety of this workshop.

:key: Keep your [AWS Cloud9 IDE](#aws-cloud9-ide) opened in a browser tab

## Installing the New Relic CLI with Cloud9

Within the shell in your Cloud9 environment, install the New Relic CLI tool by executing the following command:

```bash
pip3 install newrelic-lambda-cli --user
```

![Xloud9 Shell](/images/getting_started/cloud9-shell-nr-cli.png)

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
