# Encoding and standard I/O

## Standard Error

* Help commands \(Like : _**`nc -h`**_\)
* Check if standard error is shown or not. \( `>/dev/null` \)
* Error redirection \( `2>&1`\)

## Standard input

* d

## Standard output

* d

## Encoding

* If the input or the output breaks, we could try to use base64 encoding to send information.

### How to Identify a base64 encoding

* Check that the length is a multiple of 4 characters
*  In base64 encoding, the character set is `[A-Z, a-z, 0-9, and + /]`. If the rest length is less than 4, the string is padded with `'='` characters.
* Regex to identify base64 encoding 
  *   ```text
    ^([A-Za-z0-9+/]{4})*([A-Za-z0-9+/]{3}=|[A-Za-z0-9+/]{2}==)?$
    ```

    d

  * d
* 
