# icloudmail

If you're an Apple iCloud+ subscriber, you can now use a custom email domain for your iCloud Mail account. This is a great way to create a more professional email address and promote your brand. However, setting up a custom domain for iCloud Mail can be a bit tricky, especially if you're not familiar with AWS Route53.

That's where this project comes in! You'll find an AWS CloudFormation template that automates the process of configuring your Route53 domain for iCloud Mail. With just a few clicks, you can have all the necessary Route53 record sets created to verify your domain ownership and set up MX routing.

To use this CloudFormation application, simply download the template from this repository and launch it in your AWS account. The template will prompt you for some basic information, such as your domain name, and then take care of the rest. **Note that domain verification can take up to 72 hours.**

## Prerequisites

- Head up to the [Apple iCloud website](https://www.icloud.com/icloudplus/customdomain) and start the configuration of your custom domain;
- Save the `apple-domain=VERIFICATION_KEY` key Apple has configured for you. This verification key is required to properly verify your domain ownership.

## Installation

### Software prerequisites

- [**AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html);
- [**AWS SAM CLI**](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-getting-started.html).

### CloudFormation / SAM configuration

#### Template parameters

This CloudFormation template requires the following parameters to be overwritten:

Parameter name                 | Required |             Value(s)             |                                                                                                                           Description
:----------------------------- | :------: | :------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------:
`AppleDomainKey`               |   Yes    |                                  |                                                    The verification key provided by Apple to verify your domain ownership.
`DomainName`                   |   Yes    |                                  |                                                                The fully qualified domain name for which record sets will be created.
`HostedZoneId`                 |   Yes    |                                  |                                                              The identifier (ID) of the AWS Route53 hosted zone for the given domain.
`TagApplication`               |    No    |    **Default:** icloudmail       |                                                            A unique, friendly name used to identify resources deployed by this stack.
`TagEnvironment`               |   Yes    |  **Allowed values:** dev / prod  |       The target environment name will be tagged to all deployed resources and used to determine environment-specific configurations.

### Deploying the application

- Build and deploy the stack with AWS SAM CLI:
  ```sh
  sam build -t icloudmail.template.yml
  sam deploy --guided
  ```
