# Verbatae: verify your download

This page publishes the fingerprint (SHA-256) of the current Verbatae beta build for Mac. It does not host the app and does not link to it. If someone gave you a copy, you can check that what you have is exactly the build that was tested and signed.

**Current build:** see [`LATEST.sha256`](LATEST.sha256). History is in [`CHECKSUMS.md`](CHECKSUMS.md).

## Check it (Terminal, about a minute)

1. Fingerprint the file you downloaded:

       shasum -a 256 ~/Downloads/Verbatae-0.1.1-arm64.dmg

   The long string it prints must be identical to the one in `LATEST.sha256`. One different character means it is not the same file.

2. Optionally, check with one command. Save `LATEST.sha256` into the same folder as the download and run:

       cd ~/Downloads && shasum -a 256 -c LATEST.sha256

   It should say `Verbatae-0.1.1-arm64.dmg: OK`.

3. Ask macOS whether it accepts the file:

       spctl -a -t open --context context:primary-signature -vv ~/Downloads/Verbatae-0.1.1-arm64.dmg

   Expected: `accepted` and `source=Notarized Developer ID`.

4. After you open the disk image, check who signed the app:

       codesign -dv --verbose=2 /Volumes/Verbatae/Verbatae.app 2>&1 | grep -E "Authority|TeamIdentifier"

   Expected: `TeamIdentifier=HQF6YRR9T7`.

## If something does not match

Do not open the app. Delete the file and tell the person who sent it to you, so they can send a fresh copy.

## What this proves, and what it does not

A matching fingerprint shows your file is byte-for-byte the build listed here. It does not say anything about a build newer than the one listed, or about files that are not the Verbatae disk image.
