# 🔐 GitHub SSH Key Setup Guide

This guide walks through generating and adding a secure SSH key for authenticating with GitHub.


ls -al ~/.ssh

ssh-keygen -t ed25519 -C <"email">

eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_ed25519

cat ~/.ssh/id_ed25519.pub

Adding the new SSH key to Github account