Setting up local Git tracking with the `obsidian-git` plugin is a fantastic choice. It keeps your files 100% private, gives you full version history, and automatically backs up your vault to GitHub in the background without needing a paid subscription.

  

Since you mentioned having multiple SSH keys, let's get your local vault initialized and connected securely step-by-step.

  

### Step 1: Initialize Git in Your Vault Folder

First, open your terminal, navigate to your Obsidian vault directory (e.g., `Dev-Academy-Vault`), and initialize a local Git repository:

  

Bash

```
cd ~/Documents/Dev-Academy-Vault   # Replace with your actual vault path
git init
```

### Step 2: Create a `.gitignore` File

Obsidian and your OS generate temporary cache files that you don't want clogging up your GitHub repository. Create a `.gitignore` file inside your vault root:

  

Bash

```
nano .gitignore
```

Paste these lines inside, save, and exit (`Ctrl+O`, `Enter`, `Ctrl+X`):

  

Plaintext

```
.obsidian/workspace
.obsidian/workspace.json
.obsidian/cache
.DS_Store
```

### Step 3: Handle Your SSH Keys (Multiple Keys Setup)

Since you have two SSH keys, you need to tell Git which key to use for this specific repository.

  

1. List your keys to check their filenames (usually in `~/.ssh/`):
    
      
    
    Bash
    
    ```
    ls -la ~/.ssh/
    ```
    
2. Identify the specific SSH key you want to use for GitHub (for example, `id_rsa_github` or `id_ed25519_github`).
    
      
    
3. Set the local SSH command specifically for _this_ vault repository so it doesn't conflict with your other keys:
    
      
    
    Bash
    
    ```
    git config core.sshCommand "ssh -i ~/.ssh/YOUR_SPECIFIC_KEY -o IdentitiesOnly=yes"
    ```
    
    _(Replace `~/.ssh/YOUR_SPECIFIC_KEY` with the exact path to your GitHub-associated private key)._
    
      
    

### Step 4: Link to Your GitHub Repository

1. Create a new **Private** repository on GitHub (e.g., named `dev-academy-vault`).
    
      
    
2. Link your local vault to GitHub and push your initial setup:
    
      
    
    Bash
    
    ```
    git remote add origin git@github.com:YOUR_USERNAME/dev-academy-vault.git
    git branch -M main
    git add .
    git commit -m "feat: initial vault structure"
    git push -u origin main
    ```
    

### Step 5: Install and Configure the `obsidian-git` Plugin

Now that your local folder is a working Git repository linked to GitHub, automate it inside Obsidian:

  

1. Open Obsidian and open your vault.
    
      
    
2. Go to **Settings** $\rightarrow$ **Community plugins** $\rightarrow$ Enable community plugins.
    
      
    
3. Click **Browse**, search for **Obsidian Git**, and click **Install**, then **Enable**.
    
      
    
4. Open the **Obsidian Git Settings**:
    
      
    - **Vault backup interval:** Set your preferred automatic backup frequency (e.g., every 30 or 60 minutes).
        
          
        
    - **Commit message:** You can customize the auto-commit message (e.g., `backup: {{date}}`).
        
          
        
    - **Pull on startup:** Toggle **On** so your vault updates automatically whenever you open Obsidian on a new device.
        
          
        
    - **Push on save:** Toggle **On** if you want your changes synced to GitHub shortly after you finish typing.