You can use a GPG key (instead of an SSH key) to authenticate an SSH session.

cf. https://opensource.com/article/19/4/gpg-subkeys-ssh

---

## Set up a key on the client

Create a GPG sub-key from your existing key:

```bash
gpg2 --expert --edit-key $KEYID
```

Then in the GPG shell:

1. `addkey`
1. Select 'RSA (set your own capabilities)'
1. 'Toggle the sign capability'
1. 'Toggle the encrypt capability'
1. 'Toggle the authenticate capability'
1. 'Finished'
1. Choose some number of bytes (e.g. 2048)
1. Choose 'key does not expire'

Unless it's enabled already, tell gpg-agent to enable ssh support:

```bash
echo enable-ssh-support >> ~/.gnupg/gpg-agent.conf
```

Optionally, specify the keys to be used for SSH so you won't have to use `ssh-add` to load the keys.

```bash
gpg --list-secret-keys --with-keygrip $KEYID
# Then copy the Keygrip from the output above to KEYGRIP
echo $KEYGRIP >> ~/.gnupg/sshcontrol
```

Tell ssh how to access the gpg-agent:

```bash
export SSH_AUTH_SOCK=$(gpgconf --list-dirs agent-ssh-socket)
gpgconf --launch gpg-agent
```

Finally, add your key to the server. You can get the public ssh key with:

```bash
ssh-add -L
```

## Extract SSH key from GPG key

As stated above, you can run `ssh-add -L` to get the public ssh key. But if you haven't gone through the entire setup above (as in the example of someone else sending you a GPG key, as qjones@espsvcs.com did to me), you can extract an ssh key with `gpg --export-ssh-key $KEYID`.

## Why GPG over SSH?

1. It allows you to set an expiration date for your key.
1. It allows you to manage your keys with a keyring and reduce the number of total keys (if you're already using GPG anyway).
