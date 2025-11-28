# yubikey

types: `resident` and `non resident`

- `resident` are descoverable key
- `non resident` keys need to be known by machine. The knowledge is placed inside small file in `.ssh` directory

```
# adding a new key
ssh-keygen -t ed25519-sk -O resident -O verify-required -C "Main Key"

# adding a new key per app
ssh-keygen -t ed25519-sk -O resident -O application=ssh:<UID> -C "My Comment"
#ssh-keygen -t ed25519-sk -O resident -O application=ssh:github -C "My Comment"
#ssh-keygen -t ed25519-sk -O resident -O application=ssh:homelab -C "My Comment"
```
