# yubikey

types: `resident` and `non resident`

- `resident` are descoverable key
- `non resident` keys need to be known by machine. The knowledge is placed inside small file in `.ssh` directory

```
# github
ssh-keygen -t ed25519-sk -O resident -O verify-required -O application=ssh:github.com-auth -C "github.com auth on key 1" -f ~/.ssh/yubikeys/1_github.com_auth
ssh-keygen -t ed25519-sk -O resident -O verify-required -O application=ssh:github.com-sign -C "github.com sign on key 1" -f ~/.ssh/yubikeys/1_github.com_sign

# gitea
ssh-keygen -t ed25519-sk -O resident -O verify-required -O application=ssh:git.optimistic.cloud-auth -C "git.optimistic.cloud auth on key 1" -f ~/.ssh/yubikeys/1_git.optimistic.cloud_auth
ssh-keygen -t ed25519-sk -O resident -O verify-required -O application=ssh:git.optimistic.cloud-sign -C "git.optimistic.cloud sign on key 1" -f ~/.ssh/yubikeys/1_git.optimistic.cloud_sign

# codeberg
ssh-keygen -t ed25519-sk -O resident -O verify-required -O application=ssh:codeberg.org-auth -C "codeberg.org auth on key 1" -f ~/.ssh/yubikeys/1_codeberg.org_auth
ssh-keygen -t ed25519-sk -O resident -O verify-required -O application=ssh:codeberg.org-sign -C "codeberg.org sign on key 1" -f ~/.ssh/yubikeys/1_codeberg.org_sign

# gitlab
ssh-keygen -t ed25519-sk -O resident -O verify-required -O application=ssh:gitlab.com-auth -C "gitlab.com auth on key 1" -f ~/.ssh/yubikeys/1_gitlab.com_auth
ssh-keygen -t ed25519-sk -O resident -O verify-required -O application=ssh:gitlab.com-sign -C "gitlab.com sign on key 1" -f ~/.ssh/yubikeys/1_gitlab.com_sign

# test on github
ssh -i keychain_git_auth -v git@github.com

git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/yubikeys/keychain_git_sign.pub
git config --global commit.gpgSign true
git config --global tag.forceSignAnnotated true
git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers

# ~/.ssh/allowed_signers
echo "your.email@example.com namespaces=\"git\" $(cat ~/.ssh/yubikeys/keychain_git_sign.pub)" > ~/.ssh/allowed_signers

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
