# Threat model

## What this project does and where untrusted input enters
Docker build recipe and entrypoint scripts for a Transmission (BitTorrent) container
(linuxserver style). Untrusted input: environment variables, bind-mounted volumes, and the
container network. The scripts are the code under review; the Transmission binary is fetched at
build time and out of scope.

## Components that matter most / least
- most: the entrypoint/startup shell scripts (command-assembly from environment variables).
- least: the Dockerfile, static config.

## How to exercise it
Run the entrypoint with hostile environment values; trace variable interpolation.

## How you rate severity
- Command injection via environment variables: high (critical if host code execution).
- Credential exposure in logs: medium.

## Anything to leave alone
- The fetched Transmission binary is out of scope for this repo.
