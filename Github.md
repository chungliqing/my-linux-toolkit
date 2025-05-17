# 🔐 GitHub SSH Key Setup Guide for Linux

This guide walks through generating and adding a secure SSH key for authenticating with GitHub.


## 🛠️ Steps

```bash
# 1. Check for existing SSH keys
ls -al ~/.ssh

# 2. Generate a new SSH key (replace with your email)
ssh-keygen -t ed25519 -C "youremail@example.com"

# 3. Start the SSH agent in the background
eval "$(ssh-agent -s)"

# 4. Add your private key to the SSH agent
ssh-add ~/.ssh/id_ed25519

# 5. Display the public key (copy this to GitHub)
cat ~/.ssh/id_ed25519.pub

Adding the new SSH key to Github account

# 🔐 GitHub SSH Key Setup Guide for Windows (Bash)
ls ~/.ssh
ssh-keygen
cat ~/.ssh/id_ed25519.pub
Adding the new SSH key to Github account

# 🔐 GitHub SSH Key Setup Guide for Windows (Bash)
git init
git add .
git commit -m "initial commit"
git remote add origin ,"Github-repo-link">
git remote -v
git branch -M main
git push -u origin main