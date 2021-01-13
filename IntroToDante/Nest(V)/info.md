# Nest

Most important for this Machine, first of all SMB scanning and pentesting. Then,
we just need to do some research over directories to find juicy content. 

## ADS (Alternate Data Streams)

This is a way to have metadata information in a file. Way to do it in:

* Create a normal file: ```echo "some visible text" > file.txt```
* Add ADS: ```echo "metadata text" > file.txt:hidden```
* Get visible content: ```type file.txt```
* Get ADS: ```more < file.txt:hidden```

In a SMB context, we can:

* Get the metadata information with: ```allinfo file.txt```
* Then we know the ADS name so we can get the file using: ```get file.txt:ADSname``` 
