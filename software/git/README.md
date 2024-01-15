# Git

# Issues
## Permission denied (publickey).
```
Permission denied (publickey).
fatal: Could not read from remote repository.
```
Occurs when git server/service does not hold a public key for the user's SSH key.

### Debugging Public Key Issue
Run `$ ssh -vT git@gitserver.com` (e.g. `$ ssh -vT git@github.com`)

`ssh` will report which shh keys are available and can connect to the git service. If all ssh keys fail or no ssh keys exists, the git service does not hold any of the user's public ssh key.
### Resolution
Provide the ssh public key to the git server/service
