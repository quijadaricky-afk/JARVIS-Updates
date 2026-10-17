# Signed release workflow

The GitHub Actions workflow is **manual**, not an unattended publisher.

1. On your own PC, create a release ZIP with the application under the `JARVIS/` directory, then sign the **exact ZIP bytes** with your existing Ed25519 publisher private key. Never upload the private key, passwords, API keys or `.env` files.
2. Add the ZIP and its base64 signature to `release-candidates/vX.Y.Z/JARVIS_vX.Y.Z_Windows.zip` and `JARVIS_vX.Y.Z_Windows.zip.sig` on the default branch.
3. In GitHub Actions, choose **Publish signed JARVIS release**, click **Run workflow**, and enter `vX.Y.Z`.
4. The workflow checks the signature against `publisher-public.pem`, validates ZIP structure, and publishes a GitHub release only if no release already exists. JARVIS will discover it on its next update check and require approval to install.

**Security:** The public key here was taken from the supplied JARVIS bundle. Before first use, confirm it matches the public key associated with the **private key on your PC**. This workflow does not sign releases, automatically create candidates, or install updates. ZIPs staged in a public repository are publicly accessible. Delete staged candidates when no longer needed.
