# Git and GitHub First-Time Setup Guide

## 1. Initial Git Configuration

After installing Git, configure your identity (required for commits):

```bash
# Set your name (use your real name)
git config --global user.name "Your Full Name"

# Set your email (use the same email as your GitHub account)
git config --global user.email "your.email@example.com"

# Set default branch name to 'main'
git config --global init.defaultBranch main

# Optional: Set your preferred text editor
git config --global core.editor "code --wait"  # For VS Code
# git config --global core.editor "nano"       # For nano
# git config --global core.editor "vim"        # For vim
```

## 2. Verify Configuration

```bash
# Check your configuration
git config --list

# Check specific settings
git config user.name
git config user.email
```

## 3. Generate SSH Key (Recommended for GitHub)

SSH keys provide secure authentication without entering passwords:

```bash
# Generate a new SSH key (replace with your GitHub email)
ssh-keygen -t ed25519 -C "your.email@example.com"

# If ed25519 is not supported, use RSA:
# ssh-keygen -t rsa -b 4096 -C "your.email@example.com"

# Start the ssh-agent
eval "$(ssh-agent -s)"

# Add your SSH private key to ssh-agent
ssh-add ~/.ssh/id_ed25519
# or for RSA: ssh-add ~/.ssh/id_rsa
```

## 4. Add SSH Key to GitHub

1. Copy your public key to clipboard:
```bash
cat ~/.ssh/id_ed25519.pub
# or for RSA: cat ~/.ssh/id_rsa.pub
```

2. Go to GitHub.com → Settings → SSH and GPG keys → New SSH key
3. Paste the key and give it a descriptive title
4. Click "Add SSH key"

## 5. Test SSH Connection

```bash
# Test your SSH connection to GitHub
ssh -T git@github.com
```

You should see a message like: "Hi username! You've successfully authenticated..."

## 6. Initialize Your First Repository

```bash
# Navigate to your project directory
cd /path/to/your/project

# Initialize a new Git repository
git init

# Create a README file
echo "# My Project" > README.md

# Add files to staging area
git add .

# Make your first commit
git commit -m "Initial commit"
```

## 7. Connect to GitHub Repository

### Option A: Create repository on GitHub first, then clone
```bash
# Clone an existing repository
git clone git@github.com:username/repository-name.git
cd repository-name
```

### Option B: Push existing local repository to GitHub
```bash
# Add remote origin (replace with your repository URL)
git remote add origin git@github.com:username/repository-name.git

# Push to GitHub
git push -u origin main
```

## 8. Essential Git Commands

### Basic Workflow
```bash
# Check status of files
git status

# Add specific files
git add filename.txt

# Add all files
git add .

# Commit changes
git commit -m "Descriptive commit message"

# Push to remote repository
git push

# Pull latest changes
git pull
```

### Branching
```bash
# Create and switch to new branch
git checkout -b feature-branch

# Switch between branches
git checkout main
git checkout feature-branch

# List all branches
git branch

# Merge branch into main
git checkout main
git merge feature-branch

# Delete branch
git branch -d feature-branch
```

### Viewing History
```bash
# View commit history
git log

# View condensed history
git log --oneline

# View changes in last commit
git show
```

## 9. Useful Git Configurations

```bash
# Enable colored output
git config --global color.ui auto

# Set up aliases for common commands
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit

# Configure line ending handling (important for cross-platform)
# On Windows:
git config --global core.autocrlf true
# On Mac/Linux:
git config --global core.autocrlf input
```

## 10. GitHub CLI (Optional but Useful)

Install GitHub CLI for easier GitHub operations:

```bash
# On Ubuntu/Debian
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh

# Authenticate with GitHub
gh auth login

# Create repository from command line
gh repo create my-project --public --push
```

## 11. .gitignore File

Create a `.gitignore` file to exclude files you don't want to track:

```bash
# Example .gitignore content
node_modules/
.env
*.log
.DS_Store
__pycache__/
*.pyc
.vscode/
```

## Common First-Time Issues and Solutions

1. **Permission denied (publickey)**: Make sure your SSH key is added to GitHub
2. **Author identity unknown**: Set your git config user.name and user.email
3. **Branch 'master' vs 'main'**: Use `git config --global init.defaultBranch main`
4. **Line ending issues**: Configure `core.autocrlf` appropriately for your OS

## Quick Start Checklist

- [ ] Install Git
- [ ] Configure user.name and user.email
- [ ] Generate SSH key
- [ ] Add SSH key to GitHub account
- [ ] Test SSH connection
- [ ] Create your first repository
- [ ] Make your first commit
- [ ] Push to GitHub

Remember to replace placeholders like "Your Full Name", "your.email@example.com", and "username/repository-name" with your actual information!