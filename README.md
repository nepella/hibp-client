# hibp-client

## A brief introduction

[Have I Been Pwned](<https://haveibeenpwned.com/>) (HIBP) is a repository of online account credentials (usernames and passwords) leaked from data breaches, published, as part of a broader security awareness effort,[1] to inform affected users and to encourage service providers to check users' passwords against ones known to be compromised.[2] As of February 2018, HIBP cataloged 501 million unique passwords.

To reduce the potential for nefarious uses, HIBP provides the breached passwords as unsalted SHA-1 hashes.[3] The list [can be downloaded](<https://haveibeenpwned.com/Passwords>) (9 GiB), queried by an API, or accessed with a Web front-end that uses the same API. Using the API does not compromise a queried password: a client computes the SHA-1 hash and sends the first 5 hexadecimal digits (20 bits) to the API endpoint; the endpoint returns a list of hashes that begin with the specified prefix. Thus, only 20 bits of the 160-bit unsalted SHA-1 hash of the password is disclosed.[4]

## pwnedcheck

pwnedcheck is a humble front-end to HIBP's password API. It reads newline-terminated passwords from STDIN and checks each against the API, printing a colon-delimited pairing of the password and the number of times it appears in HIBP's database. It returns non-zero if any candidate is matched.

### Example usage

    nepeta@garden:hibp-cleint $ echo -e 'pa$$w0rd7\nbunnybunnybunny\nqelhajminq' | ./pwnedcheck
    pa$$w0rd7:12
    bunnybunnybunny:20
    qelhajminq:0

    nepeta@garden:hibp-client $ echo "PassW0rd!" | ./pwnedcheck >/dev/null || echo "The password is compromised."
    The password is compromised.

## Footnotes

1. Troy Hunt, *[Passwords Evolved: Authentication Guidance for the Modern Era](<https://www.troyhunt.com/passwords-evolved-authentication-guidance-for-the-modern-era/>)* (July 26, 2017).

2. Troy Hunt, *[Introducing 306 Million Freely Downloadable Pwned Passwords](<https://www.troyhunt.com/introducing-306-million-freely-downloadable-pwned-passwords/>)* (Aug. 3, 2017); Troy Hunt, *[We're Baking Have I Been Pwned into Firefox and 1Password](<https://www.troyhunt.com/were-baking-have-i-been-pwned-into-firefox-and-1password/>)* (June 26, 2018).

3. *See id.* § Why hashes?

4. Troy Hunt, *[Enhancing Pwned Passwords Privacy by Exclusively Supporting Anonymity](<https://www.troyhunt.com/enhancing-pwned-passwords-privacy-by-exclusively-supporting-anonymity/>)* (Apr. 28, 2018).

## References

* [APIv2](<https://haveibeenpwned.com/API/v2#PwnedPasswords>), Have I Been Pwned.
