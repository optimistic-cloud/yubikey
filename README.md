# yubikey

types: `resident` and `non resident`

- `resident` are descoverable key
- `non resident` keys need to be known by machine. The knowledge is placed inside small file in `.ssh` directory

```
# adding a new key
ssh-keygen -t ed25519-sk -O resident -O verify-required -C "Git SSH key"
ssh-keygen -t ed25519-sk -O resident -O application=ssh:git -O verify-required -C "Git SSH Key" -f ~/.ssh/id_ed25519_sk_git

# adding a new key per app
ssh-keygen -t ed25519-sk -O resident -O application=ssh:<UID> -C "My Comment"
#ssh-keygen -t ed25519-sk -O resident -O application=ssh:github -C "My Comment"
#ssh-keygen -t ed25519-sk -O resident -O application=ssh:homelab -C "My Comment"

# signing key
# https://developers.yubico.com/SSH/Securing_git_with_SSH_and_FIDO2.html
ssh-keygen -t ed25519-sk -O resident -O application=ssh:git-sign -O verify-required -C "Git Signing Key" -f ~/.ssh/id_ed25519_sk_git_sign
```

```
ykman fido credentials list
```
