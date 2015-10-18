#Secure Notes

This utility attempts to make GPG encryption considerably easier to use within a set group of users.

##Installation
1. Run the provided install script:
  `./install`
1a. If you would like to specify a custom keystore repository, set it as the first argument:
  `./install foobar/keystore`

##Usage
This tool will try to figure out what you are intending to do by what data you
put in. No flags are necessary. Data can be provided by the clipboard, typing
in manually, via pipes with stdin or a file. In order to encrypt data the
identity of a person is required, as well as a message to encrypt. Please see
the examples below.

NOTE: All data is output to the console on stdout as well as to your clipboard if it is accessible.

Please see the usage examples below:

NOTE: In relation to the examples below, an ID for a person can be any of the following:
  - A full email address
  - The start of a person's email address (e.g. 'justin' will match 'justin@c9.io')
  - A GPG key ID (This can be used to send to people not registered in the keystore)

###Decrypting data
  From the clipboard:
  `secnotes`

  From a file:
  `secnotes ENCRYPTED_FILE`

  From stdin:
  echo '[ENCRYPTED DATA]' | secnotes

###Encrypting data
  From the clipboard:
  `secnotes ID

##Administration Details
When a user runs the install script, or manually creates a new GPG key pair,
the tool will automatically create a branch on the git repository and push their
new key under the name of the email entered during install. Please follow the below steps to set up trust of a new user's key for everyone using the tool:

1. Check the key for the user and make sure it is legitimate, the user is who they
say they are, and that they were the ones to push the new or updated key
2. Merge the branch in to master
3. Copy the user's key ID (the contents of their merge)
4. Run this on a machine with the master signing key:

##TODO
TODO: Script for signing new keys, pushing them and accepting the merge request? Can we make certain users able to push to master on github?
TODO: For the admin side; is it possible to create a pull request via CLI to github?
TODO: Put this script as a webhook on keystore github?

TODO: Write a readme
TODO: only copy to clipboard if message is below some size! Large binary blobs could be encrypted with this
TODO: Move out functions in admin tool to a shared library

TODO: keybase integration?

##Notes for development
- All functions must be pipeable; anything informational should be on stderr, only actual data should be on stdout


##Allowed Invocation methods
Test Inputs                                  Expected outcome
     enc message on stdin                    decrypt stdin message
     enc message file as $1                  decrypt $1
     enc message on clipboard                decrypt clipboard
     unenc message on stdin, ID on $1        encrypt for ID
     unenc message file as $1, ID as $2      encrypt message for ID $2
     unenc message file as $2, ID as $1      encrypt message for ID $1
     unenc message on clipboard              encrypt clipboard contents
     nothing                                 ask user for data to decrypt
     ID as $1                                ask user for data to encrypt

##Errors
Test Inputs                                  Expected outcome
     unenc message on stdin                  error; no ID specified
     unenc message file as $1                error; no ID specified
