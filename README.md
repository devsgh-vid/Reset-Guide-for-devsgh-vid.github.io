# Complete Reset Guide for devsgh-vid.github.io

## IMPORTANT: Execute in This Exact Order

### Phase 1: Local Cleanup (Do This First)
**📍 Location: Ubuntu Desktop → Gnome Terminal**

**Step 1: Remove Local Repository**
**📍 Location: Ubuntu Terminal**
```bash
cd ~
rm -rf ~/Documents/devsgh-vid.github.io
```

**Step 2: Clean Ruby/Jekyll Environment**
**📍 Location: Ubuntu Terminal**
```bash
# Remove Jekyll and Bundler gems
gem uninstall jekyll bundler 2>/dev/null || true
sudo gem uninstall jekyll bundler 2>/dev/null || true

# Clean up remaining gems
gem cleanup 2>/dev/null || true
```

**Step 3: Remove rbenv Ruby Installation**
**📍 Location: Ubuntu Terminal**
```bash
# Remove specific Ruby version
rbenv uninstall 3.2.2 2>/dev/null || true

# Remove entire rbenv directory
rm -rf ~/.rbenv
```

**Step 4: Remove Node.js (NVM) Installation**
**📍 Location: Ubuntu Terminal**
```bash
# Remove specific Node.js version
nvm uninstall 18 2>/dev/null || true

# Remove entire NVM directory
rm -rf ~/.nvm
```

**Step 5: Clean Shell Configuration**
**📍 Location: Ubuntu Terminal**
```bash
# Create backup
cp ~/.bashrc ~/.bashrc.backup

# Remove rbenv and NVM lines from bashrc
sed -i '/rbenv/d' ~/.bashrc
sed -i '/nvm/d' ~/.bashrc
sed -i '/NVM_DIR/d' ~/.bashrc

# Reload shell configuration
source ~/.bashrc
```

**Step 6: Remove Development Packages**
**📍 Location: Ubuntu Terminal**
```bash
sudo apt remove -y git curl wget build-essential zlib1g-dev libssl-dev libreadline-dev libyaml-dev libffi-dev libgdbm-dev libncurses5-dev libgmp-dev autoconf bison libgdbm-compat-dev libsqlite3-dev

# Clean up unused packages
sudo apt autoremove -y
sudo apt autoclean
```

**Step 7: Clean Git Configuration**
**📍 Location: Ubuntu Terminal**
```bash
git config --global --unset user.name 2>/dev/null || true
git config --global --unset user.email 2>/dev/null || true
git config --global --unset init.defaultBranch 2>/dev/null || true
```

### Phase 2: GitHub Repository Deletion (Do This After Local Cleanup)
**📍 Location: Web Browser (Chrome, Firefox, etc.)**

**Step 8: Delete GitHub Repository (Manual)**
**📍 Location: Web Browser (Any browser - Chrome, Firefox, Edge, etc.)**
1. Open your web browser
2. Go to `https://github.com/devsgh-vid/devsgh-vid.github.io`
3. Click on **Settings** tab
4. Scroll down to **Danger Zone** section
5. Click **"Delete this repository"**
6. Type: `devsgh-vid/devsgh-vid.github.io` to confirm
7. Click **"I understand the consequences, delete this repository"**

### Phase 3: Final Verification and System Update
**📍 Location: Ubuntu Desktop → Gnome Terminal**

**Step 9: Verify Complete Cleanup**
**📍 Location: Ubuntu Terminal**
```bash
# Check if Ruby is removed
ruby -v
# Should show "command not found" or system Ruby

# Check if Node.js is removed
node -v
# Should show "command not found"

# Check if Jekyll is removed
jekyll -v
# Should show "command not found"

# Check if local repo is gone
ls ~/Documents | grep devsgh-vid
# Should return nothing

# Check Git config is clean
git config --global --list
# Should show minimal or no configuration
```

**Step 10: Final System Update**
**📍 Location: Ubuntu Terminal**
```bash
sudo apt update
sudo apt upgrade -y
```

## Critical Timing Notes:

- **Complete Steps 1-7 locally BEFORE deleting the GitHub repository**
- **Delete the GitHub repository (Step 8) only after local cleanup is complete**
- **The repository will be completely gone after Step 8 - no recovery possible**

## Expected Final State:

✅ No local repository files  
✅ No Ruby/Jekyll installation  
✅ No Node.js installation  
✅ No development packages  
✅ Clean shell configuration  
✅ No GitHub repository  
✅ System ready for fresh start from Step 1

## If Something Goes Wrong:

If you encounter errors during cleanup, you can use the "Nuclear Option":
**📍 Location: Ubuntu Terminal**
```bash
# Complete system reset (use with caution)
rm -rf ~/.rbenv ~/.nvm
rm -rf ~/Documents/devsgh-vid.github.io
sudo apt remove -y git curl wget build-essential zlib1g-dev libssl-dev libreadline-dev libyaml-dev libffi-dev libgdbm-dev libncurses5-dev libgmp-dev autoconf bison libgdbm-compat-dev libsqlite3-dev
sudo apt autoremove -y && sudo apt autoclean
```

**Warning: After completing all steps, the repository `devsgh-vid.github.io` will be permanently deleted and cannot be recovered. Make sure you have backups of any important data before proceeding.**
