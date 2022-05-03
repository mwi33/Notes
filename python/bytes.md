# Working with bytes
## Introduction
## Process
``` mermaid

graph LR

    String --> Bytes

    String --> Hex

    Bytes --> Bin_Dec

    Bytes --> Bin

    Bin --> Pad_trim

    Pad_trim --> join_string

    Hex --> Base64

    Hex --> Bytes

```

## Functions
### Convert string to bytes 'utf-8'
``` python

message_bytes = bytes(message, 'utf-8')

```

### Convert string to hex
``` python

message_bytes_hex = bytes(message, 'utf-8').hex()

```

### Convert bytes to the decimal representation of binary

``` python

message_bin_dec = [bit for bit in message_bytes]

```

### Convert bytes to binary

``` python

message_bin = [bin(bit) for bit in message_bytes]

```

### Remove leading 0b from binary string
``` python

# removes the leading 0b characters and pads to 8 bits

  

message_bin_trim_pad = [bit[2:].zfill(8) for bit in message_bytes_bin]

  

```

### Convert the list into a continious string
``` python

binary_string = "".join([str(bit) for bit in message_bin_trim_pad])

```

### Convert hex to base64
``` python

import base64

  

base64_encoded = base64.b64encode(bytes.fromhex(message_bytes_hex))

```

### Convert hex to bytes
``` python

bytes_string = bytes.fromhex(message_bytes_hex)

```