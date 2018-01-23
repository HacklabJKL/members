# Hacklab member hashmap tools

Every time our private membership repository changes, we generate HMAC
using SHA-256 hash function from all of our members' email addresses.

It is uUseful for giving discounts to some services without
revealing the membership registry open to the Internet. Only the
number of members is shown. When you know the HMAC, it is possible to
check a membership but not decode full contents of the registry.

Every service has its own hash map

## File format

Hash file contains a number of 256 bit (32 byte) HMAC hashes of member
email addresses sorted by the raw hash value. The file is pure binary
for added epicness.

Email addresses are normalized using the following algorithm:

1. Trim whitespace
1. Convert to lowercase
1. Remove `+` aliases from the address (e.g. user+something@example.com → user@example.com)
1. Calculate HMAC from the email using given hmac key

See [tools/check](tools/check) for reference implementation

To compare, check the normalized email address against each 32 byte entry.
