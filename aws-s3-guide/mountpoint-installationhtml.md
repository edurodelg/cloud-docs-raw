---
source_url: https://docs.aws.amazon.com/AmazonS3/latest/userguide/mountpoint-installation.html
fetched_at: 2026-02-02T15:52:22.070133
---

# Installing Mountpoint

You can download and install prebuilt packages of Mountpoint for Amazon S3 by using the command line. The instructions for downloading and installing Mountpoint vary, depending on which Linux operating system that you're using.

###### Topics

## Amazon Linux 2023 (AL2023)

Mountpoint is available directly in the Amazon Linux 2023 repository since AL2023 version 2023.9.20251110.

-
Install it by entering the following command:

`sudo dnf install mount-s3`

-
Verify that Mountpoint for Amazon S3 is successfully installed:

`mount-s3 --version`

You should see output similar to the following:

`mount-s3 1.21.0+1.amzn2023`


## Other RPM-based distributions (Amazon Linux 2, Fedora, CentOS, RHEL)

-
Copy the following download URL for your architecture.

*x86_64*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.rpm`

*ARM64 (Graviton)*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/arm64/mount-s3.rpm`

-
Download the Mountpoint for Amazon S3 package. Replace


with the appropriate download URL from the preceding step.`download-link`

`wget`

`download-link`

-
(Optional) Verify the authenticity and integrity of the downloaded file. First, copy the appropriate signature URL for your architecture.

*x86_64*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.rpm.asc`

*ARM64 (Graviton)*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/arm64/mount-s3.rpm.asc`

Next, see

[Verifying the signature of the Mountpoint for Amazon S3 package](#mountpoint-install-verify). -
Install the package by using the following command:

`sudo yum install ./mount-s3.rpm`

-
Verify that Mountpoint is successfully installed by entering the following command:

`mount-s3 --version`

You should see output similar to the following:

`mount-s3 1.21.0`


## DEB-based distributions (Debian, Ubuntu)

-
Copy the download URL for your architecture.

*x86_64*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.deb`

*ARM64 (Graviton)*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/arm64/mount-s3.deb`

-
Download the Mountpoint for Amazon S3 package. Replace


with the appropriate download URL from the preceding step.`download-link`

`wget`

`download-link`

-
(Optional) Verify the authenticity and integrity of the downloaded file. First, copy the signature URL for your architecture.

*x86_64*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.deb.asc`

*ARM64 (Graviton)*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/arm64/mount-s3.deb.asc`

Next, see

[Verifying the signature of the Mountpoint for Amazon S3 package](#mountpoint-install-verify). -
Install the package by using the following command:

`sudo apt-get install ./mount-s3.deb`

-
Verify that Mountpoint for Amazon S3 is successfully installed by running the following command:

`mount-s3 --version`

You should see output similar to the following:

`mount-s3 1.21.0`


## Other Linux distributions

-
Consult your operating system documentation to install the

`FUSE`

and`libfuse2`

packages, which are required. -
Copy the download URL for your architecture.

*x86_64*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.tar.gz`

*ARM64 (Graviton)*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/arm64/mount-s3.tar.gz`

-
Download the Mountpoint for Amazon S3 package. Replace


with the appropriate download URL from the preceding step.`download-link`

`wget`

`download-link`

-
(Optional) Verify the authenticity and integrity of the downloaded file. First, copy the signature URL for your architecture.

*x86_64*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.tar.gz.asc`

*ARM64 (Graviton)*:`https://s3.amazonaws.com/mountpoint-s3-release/latest/arm64/mount-s3.tar.gz.asc`

Next, see

[Verifying the signature of the Mountpoint for Amazon S3 package](#mountpoint-install-verify). -
Install the package by using the following command:

`sudo mkdir -p /opt/aws/mountpoint-s3 && sudo tar -C /opt/aws/mountpoint-s3 -xzf ./mount-s3.tar.gz`

-
Add the

`mount-s3`

binary to your`PATH`

environment variable. In your`$HOME/.profile`

file, append the following line:`export PATH=$PATH:/opt/aws/mountpoint-s3/bin`

Save the

`.profile`

file, and run the following command:`source $HOME/.profile`

-
Verify that Mountpoint for Amazon S3 is successfully installed by running the following command:

`mount-s3 --version`

You should see output similar to the following:

`mount-s3 1.21.0`


## Verifying the signature of the Mountpoint for Amazon S3 package

-
Install GnuPG (the

`gpg`

command). It is required to verify the authenticity and integrity of a downloaded Mountpoint for Amazon S3 package. GnuPG is installed by default on Amazon Linux Amazon Machine Images (AMIs). After you installGnuPG, proceed to step 2. -
Download the Mountpoint public key by running the following command:

`wget https://s3.amazonaws.com/mountpoint-s3-release/public_keys/KEYS`

-
Import the Mountpoint public key into your keyring by running the following command:

`gpg --import KEYS`

-
Verify the fingerprint of the Mountpoint public key by running the following command:

`gpg --fingerprint mountpoint-s3@amazon.com`

Confirm that the displayed fingerprint string matches the following:

`673F E406 1506 BB46 9A0E F857 BE39 7A52 B086 DA5A`

If the fingerprint string doesn't match, do not finish installing Mountpoint, and contact

[AWS Support](https://aws.amazon.com/premiumsupport/). -
Download the package signature file. Replace


with the appropriate signature link from the preceding sections.`signature-link`

`wget`

`signature-link`

-
Verify the signature of the downloaded package by running the following command. Replace


with the file name from the previous step.`signature-filename`

`gpg --verify`

`signature-filename`

For example, on RPM-based distributions, including Amazon Linux, enter the following command:

`gpg --verify mount-s3.rpm.asc`

-
The output should include the phrase

`Good signature`

. If the output includes the phrase`BAD signature`

, redownload the Mountpoint package file and repeat these steps. If the issue persists, do not finish installing Mountpoint, and contact[AWS Support](https://aws.amazon.com/premiumsupport/).The output may include a warning about a trusted signature. This does not indicate a problem. It only means that you have not independently verified the Mountpoint public key.