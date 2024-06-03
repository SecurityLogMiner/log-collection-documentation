Getting Started
================
System Management Software provides the insight needed to secure, troubleshoot, and optimize systems and applications. 
Whether it is an individual user or larger organization, log collection is the first step in the analysis process. 
The collection and storage of system and application logs is designed with ease-of-use in mind to provide simple and efficient event visibiilty for any device.



Creating an Account
--------------------------
The log collection client will require an Amazon Web Services account to access the centralized server.
.. _Create an AWS account: https://portal.aws.amazon.com/billing/signup#/start/email

Set up the Identity and Access Management account privileges as a user.
    Copy your credentials such as your AWS access key and AWS secret access key

Store these variables into ~/.aws/credentials
.. code-block::
    [default] 
    aws_access_key_id=YOUR-ACCESS-KEY
    aws_secret_access_key=YOUR-SECRET-KEY

Installation
------------------
First off, clone the client

.. code-block::
    git clone https://github.com/SecurityLogMiner/log-collection-client.git

Run the install script to install client dependencies usch as AWS CLI, Terraform and Rust Programming Language
.. code-block::
    ./install.sh
Use the Terraform to create the user profile and grant proper permissions to access the client.
.. code-block::
    terraform init
    terraform plan
    terraform apply

Running the Client
-------------------------------
Start the log collector through Rust 
.. code-block::
    cd log-collection-client
    cargo install
    cargo run
Note: Be sure to activate the Rust environment by configuring the PATH environment variable Configuring the PATH environment variable

Currently, the log collector can:
- Start Log Collection
- Stop Log Collection
- View running logs
- Manage Log Collection configuration

Configuration Guidelines
-------------------------------
Configure toml file The client will have a default toml file that seeks configurations. 
Specify what log files the client will look for and what AWS DynamoDB table you'd like to store them in. 
The formatting for the toml file is as follows:
.. code-block::
    #default.toml
    [[dynamodb.package]]
    source = "<Source-file>"
    table = "<Table-name>"

