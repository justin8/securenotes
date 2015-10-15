TODO: record list of key fingerprints along with emails and store them somewhere securely; in the repo?
	- save it in a config file?
	- how to update this.
	- Maybe just store the repo location in a config file in ~/.config or ~/Library
		- Then pull from that repo; store keys with email,fingerprint format one per line? attempt to git clone on start
		- function to set the repo; shorthand for github repos?

TODO: encrpytion
TODO: decryption keyid checks
TODO: Readme



Download a master key; use it to sign other keys: 6D806CDF
trust that master key during init()
when generating key, put a message saying to request it to get trusted by ops@c9.io


recv-keys always; in case of trust updates


Warnings about untrusted keys will be handled by the gpg trust mechanism