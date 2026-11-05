# Security

- Every release is **signed** with the developer's private key (ECDSA P-256). The app checks the signature and the
  SHA-256 of the download before it installs an update; nothing is installed without your click.
- The SHA-256 of every release file is published next to it (`.sha256`). To check a download yourself in
  PowerShell: `Get-FileHash .\RevitBatchStudio-<version>.exe`.
- Found a security problem? Please contact the developer privately on
  [LinkedIn](https://www.linkedin.com/in/osmanz/) instead of opening a public issue.
