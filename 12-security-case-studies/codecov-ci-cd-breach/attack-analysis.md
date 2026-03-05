# Attack Analysis

The attack targeted the CI/CD pipeline integration used by Codecov customers.

Attackers gained unauthorized access to Codecov's infrastructure and modified a script used by customers to upload code coverage results.

The malicious script contained a command that collected environment variables from CI/CD pipelines and sent them to an attacker-controlled server.

Because the script executed during builds, the attack exposed:

- API tokens
- cloud credentials
- repository access tokens
- deployment secrets

## Attack Steps

1. Attacker compromises Codecov infrastructure
2. Bash uploader script modified with malicious code
3. Modified script distributed to customers
4. CI/CD pipelines execute the script during builds
5. Environment variables and secrets exfiltrated
6. Attackers gain access to downstream infrastructure
