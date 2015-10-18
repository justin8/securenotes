= TODO =
TODO: Script for signing new keys, pushing them and accepting the merge request? Can we make certain users able to push to master on github?
TODO: For the admin side; is it possible to create a pull request via CLI to github?
TODO: Put this script as a webhook on keystore github?

TODO: Update readme
TODO: Check clipboard functions; do we decrypt in place? same for encryption
TODO: only copy to clipboard if message is below some size! Large binary blobs could be encrypted with this
TODO: Fix key generation to be betterer
TODO: gpg/gpg2 usage; why did gpg2 break suddenly for ubuntu. Can I just use gpg?

TODO: keybase integration?

= Notes for development =
- All functions must be pipeable; anything informational should be on stderr, only actual data should be on stdout


= Allowed Invocation methods =
Test Inputs                                  Expected outcome
#    enc message on stdin                    decrypt stdin message
#    enc message file as $1                  decrypt $1
     enc message on clipboard                decrypt clipboard
#    unenc message on stdin, ID on $1        encrypt for ID
#    unenc message file as $1, ID as $2      encrypt message for ID $2
#    unenc message file as $2, ID as $1      encrypt message for ID $1
     unenc message on clipboard              encrypt clipboard contents
#    nothing                                 ask user for data to decrypt
#    ID as $1                                ask user for data to encrypt

= Errors =
Test Inputs                                  Expected outcome
#    unenc message on stdin                  error; no ID specified
#    unenc message as $1                     error; no ID specified
