 uup# Purpose
A checksum is a reliable method for verifying that two digitial items are identical.  The most relevant use case for this is to verify that a downloaded file has been transfered without error or unauthorised changes.  

At a high-level when a file is created a cryptograpic hash is created by [[Hashing]] the file.  Depending on the type of hashing algorythm used, the product of the algorythm, which is technically called the 'message digest' , although frequently referred to as the hash is created.  The hash is a fixed length hexadecimal string.

Often when a file is provided for download it includes the checksum (hash).  Once the file has been downloaded, the same cryptograpich hashing algorythm can be applied to it to obtain the hash of the downloaded file.  These two (provided hash and independently create hash) hashes are compared, if they match then we can be confident that the two files (remote and local downloaded) are identical.