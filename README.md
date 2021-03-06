# README
# Cryptez
# Jamie Carranza (gojamiegirl@gmail.com)
# August 14, 2010

Cryptez is a script that makes it easy to maintain encrypted text files.

Tilde expansion for configuration variables (e.g. ENC_DIR) only works when unquoted


HOWTO

  --> Create New Encrypted File

	cryptez -e -f <new text file>

  --> Open Plain Text File

	cryptez -f <text file>

  --> Open an encrypted file read-only

	cryptez -f <encrypted file>

  --> Open an encrypted file for editing

	cryptez -e -f <encrypted file>


OVERVIEW

  The default editor is vim  so at least basic knowledge of it's operation
  is required.  Cryptez has so far only been tested on vi

  Cryptez will search in the configured encrypted file directory, then in the
  current working directory for the input file.  If an absolute path is given
  it will be used directly.

  If the specified file does not exist and the edit option ('-e') is
  chosen a new file is created in the configured encrypted file directory.
  If the edit option is not chosen and the specified file does not exist
  Cryptez will fail.

  If the specified file exists, is not encrypted, and the edit option is chosen
  Cryptez will open the file with the configured editor in read-write mode and
  encrypt the file upon closing.  If the edit option is not chosen Cryptez will
  return an error saying that the file does not exist and exit.

  If the edit option is used Cryptez will open the input file read-write mode,
  decrypting if necessary and encrypting upon closing.  The file will be
  created in the configured encrypted file directory if it does not exist.

  If the edit option is not chosen an existing file will be opened read-only,
  decrypted if necessary.  Cryptez will return an error if the specified file
  does not exist and the edit is not chosen.


--> Each time Cryptez encrypts a file the password will be reset


SECURITY

  While a file is opened for reading or editing it exists as a plain
  text file and another user or process could potentially read or copy the file during
  this time.  This risk can be reduced 

  * Cryptez attempts to delete decrypted files upon closing a 
  document but it is possible for a file to be missed.

  Make sure decrypted files have the minimum permissions necessary.

  by using a ramdisk (volitile filesystem in memory)

  Depending on the editor used, the way to close the file may differ.


I don't know how well this works with anything other than vim

You can create a ramdisk simply by mounting an empty directory with the 'tmpfs' type.

mount -t tmpfs -o size=32M tmpfs /mnt/ramdisk

DISCLAIMER

  I'm by no means a security expert, use this software at your own risk.

  As this is alpha software, there is some potential to lose data; it's
  possible during error conditions for your input file to be deleted.

