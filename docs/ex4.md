# No. 4 SSH-Agent Installation

## Step 1: Check if ssh-agent is Installed

Run:

```tf
which ssh-agent
```

- If it shows a path like /usr/bin/ssh-agent, it’s installed.
- If not, install it:

```tf
sudo apt install openssh-client
```

## Step 2: Start ssh-agent

Start the agent in the background:

```tf
eval "$(ssh-agent -s)"
```

This sets environment variables so your shell can communicate with it.

## Step 3: Add Your Private Key

```tf
ssh-add ~/.ssh/id_rsa
```

(Use the private key file corresponding to the public key you uploaded earlier.)

## Step 4: Test with Multiple SSH Connections

- Connect to your server as before:

```tf
ssh root@162.55.178.186
```

- The ssh-agent will handle the key, so you won’t need to re-enter it for subseque-nt connections.
