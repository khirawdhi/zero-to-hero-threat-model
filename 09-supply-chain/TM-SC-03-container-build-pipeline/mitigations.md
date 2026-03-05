# Mitigations

## Base Image Security

- use trusted base image sources
- maintain allowlist of approved base images
- regularly update base images

## Build Environment Security

- isolate container build environments
- run builds with minimal privileges
- restrict network access during builds

## Image Integrity

- sign container images
- verify image signatures before deployment
- enforce immutable image tags

## Secrets Management

- avoid embedding secrets in container images
- use secure secrets management solutions
- ensure secrets are not exposed in build logs

## Container Image Scanning

- perform vulnerability scanning of images
- enforce security policy checks before deployment
- monitor container registries for suspicious images
