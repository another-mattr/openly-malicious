# Do you trust open source?

Open source is amazing. We don't have to place blind trust on the maintainers. We can read and verify the code for ourselves... or _can we_?

## Consider this repository

This is a simple repository. It does three things:

1. It generates a simple "Hello world 👋" program. [source](/.github/workflows/build_and_release.yml#L15-L16)
2. It cryptographically signs that program to ensure validity. [source](/.github/workflows/build_and_release.yml#L17-L19)
3. It uploads that program and its signature as a release on the repository. [source](/.github/workflows/build_and_release.yml#L20-L27)

Look at the code and verify for yourself. No funny business, right?

Not quite.

## This repository injects unexpected code into the build

Take a look at the `program.sh` from the latest release. There's a little more than "Hello world 👋" in there.

Do you think you could catch this in a code review? I doubt it. 😈

<details>
<summary>How to verify the signature 👇</summary>

Here's my public key:

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA7x/VH2ZDSJrG+RJBkjNP
Ihv5u7eqBMOaYyvsEQkeP7HtM+zXoyRXrqD4Yu9Y5jhXy56R5rtYryX9pVEnmdiX
T1x0FR/D0B8k7Mq7VZYw+NiCngvKVf/PVXvuPMaYSymBM9ed2nSiuMr9bkQIFHoH
x2Xji3dwFKV/n5SfPKmBAY/1azClTouC1wB9Bk0D6rXZD+aFLWGpr5kidogjk6M0
vtm+vJwY0AtPMtqSTHBXy2D1yR+//4HhybZ6u9U+zJowIR+xec7mJmN88g12kI+D
Y4o3/FGN+IlIgKQA9uv0EyfHPPZ++WawR9QgCoSazUfEb08gbM8n8iMpk5G8svX7
PQIDAQAB
-----END PUBLIC KEY-----
```

And here's the command you would run to verify:

```bash
openssl dgst -sha256 -verify public_key.pem -signature signature.sig program.sh
```
</details>


