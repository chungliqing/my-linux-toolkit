[GitHub SSH Key Setup Guide for Linux](#github-ssh-key-setup-guide-for-linux)

[GitHub SSH Key Setup Guide for Windows (Bash)](#github-ssh-key-setup-guide-for-windows-bash)

[Push Local Git Repository to Github](push-local-git-repository-to-github)

# GitHub SSH Key Setup Guide for Linux

This guide walks through generating and adding a secure SSH key on Kali Linux for authenticating with GitHub.


```bash
# 1. Check for existing SSH keys
ls -al ~/.ssh

# 2. Generate a new SSH key
ssh-keygen -t ed25519 -C "email"

# 3. Start the SSH agent in the background
eval "$(ssh-agent -s)"

# 4. Add private key to the SSH agent
ssh-add ~/.ssh/id_ed25519

# 5. Display the public key and copy it
cat ~/.ssh/id_ed25519.pub
```

\# 6. Add the new Public Key to GitHub Account
- Go to GitHub > Settings > SSH and GPG keys
- Click "New SSH key"
- Give it a descriptive title (e.g., "Kali Laptop" or "Main Dev Machine")
- Paste the entire contents of id_ed25519.pub
- Click Add SSH key

# GitHub SSH Key Setup Guide for Windows (Bash)

```bash
# 1. Check for existing SSH keys
ls ~/.ssh

# 2. Generate a new SSH key
ssh-keygen

# 3. Display the public key and copy it
cat ~/.ssh/id_ed25519.pub
```

\4. Add the new Public Key to GitHub Account
- Go to GitHub > Settings > SSH and GPG keys
- Click "New SSH key"
- Give it a descriptive title (e.g., "Kali Laptop" or "Main Dev Machine")
- Paste the entire contents of id_ed25519.pub
- Click Add SSH key

# Push Local Git Repository to Github
```bash
git init
git add .
git commit -m "initial commit"
git remote add origin "github-repo-link">
git remote -v
git branch -M main
git push -u origin main
```
