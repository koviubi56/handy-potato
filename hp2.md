# Handy Potato: 2 - PGP public key publication

Version 2

## Abstract

To make sure that sharing PGP public keys and its changes are standardized, we are creating this standard. This standard covers how to publish PGP public keys, and its changes, and other things.

## Specification

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all capitals, as shown here.

An implementation is not compliant if it fails to satisfy one or more of the MUST or REQUIRED level requirements. An implementation that satisfies all the MUST or REQUIRED level and all the SHOULD level requirements is said to be "unconditionally compliant"; one that satisfies all the MUST level requirements but not all the SHOULD level requirements is said to be "conditionally compliant."

This standard is case-sensitive.

An example implementation of the most recent version of this standard can be seen [here](https://gist.github.com/koviubi56/febdff17cc3bf59e00db73c4f87f420f).

## The file

The name of the file that is going to be used (the "File") MUST be `pgp-hp2.md`. It MUST be valid markdown, and it MUST be encoded in utf-8.
The order of the contents of the File MUST match the order within this standard.
Other things not explicitly allowed by this standard MUST NOT be present in the File.

### Current PGP public key

The following lines MUST be present in the File (backslashes MUST NOT be included; things within `<>` MUST be replaced appropriately):

```markdown
# PGP public key v1

## Current PGP public key

\```text
<ASCII armored PGP public key>
\```
```

If there are multiple PGP public keys, there MUST be a new line, and the above syntax MUST be used for every single PGP public key.

PGP public keys that are not trusted MUST NOT be listed.

### Canary

The following lines MAY be present in the File (backslashes MUST NOT be included; including empty new lines; things within `<>` MUST be replaced appropriately):

```markdown

## Canary

\```text
<
A PGP clear text signature of the following text (things within <> MUST be replaced appropriately):
I am in control of my PGP key.
I will update this canary within 14 days.
Today is <YYYY-MM-DD>.
Latest bitcoin block hash: <Latest bitcoin block hash>
>
\```
```

The PGP clear text signature MUST be signed by any of the keys within "Current PGP public key". The canary MUST NOT be repeated for every single PGP key.

Please note, that this canary is OPTIONAL. If you choose to include it, then you MUST include everything, and if you choose to not include it, then you MUST NOT include anything about the canary stated above.

### Revoked keys

The following lines MUST be present in the File (backslashes MUST NOT be included; including empty new lines; things within `<>` MUST be replaced appropriately):

```markdown

## Revoked PGP public keys

I hereby revoke all previous PGP keys associated with my identity.
Do not encrypt communications to my old keys. If you send me messages encrypted to an old key I will not read them.

- `<The PGP key's full fingerprint consisting of 40 characters>`
```

If there are multiple PGP public keys, the above syntax MUST be used for every single PGP public key.

An empty new line MUST be at the end of the File.
