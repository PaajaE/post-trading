# Change Management Workflow for Dual Repositories

## Your Current Setup

- **Czech Repository**: `uctujtrading.cz` (main repository)
- **English Repository**: `post-trading.com` (English version)

## How to Make Changes

### 1. **Common Files Changes** (Styles, Scripts, Assets)

These files are shared between both repositories:

**Files to sync:**
- `styles.css`
- `script.js` 
- `cookie-consent.js`
- `config.js`
- `assets/` folder
- `CNAME`
- Documentation files

**Workflow:**
```bash
# 1. Edit files in Czech repository
# 2. Sync to English repository
./sync-repos.sh sync-common

# 3. Commit and push both repositories
git add .
git commit -m "Update common files"
git push

# Then in English repository:
cd ../post-trading-en
git add .
git commit -m "Sync common files from Czech repo"
git push
```

### 2. **Content Changes** (Text, Images, Structure)

**Czech content:**
- Edit `index.html` in Czech repository
- Edit `en/index.html` for English content

**Workflow:**
```bash
# 1. Edit Czech content in index.html
# 2. Edit English content in en/index.html
# 3. Update English repository
./sync-repos.sh update-en

# 4. Commit and push both repositories
git add .
git commit -m "Update content"
git push

# Then in English repository:
cd ../post-trading-en
git add .
git commit -m "Update content from Czech repo"
git push
```

### 3. **New Features or Major Changes**

**Workflow:**
```bash
# 1. Create backup first
./sync-repos.sh backup

# 2. Make changes in Czech repository
# 3. Test both versions locally

# 4. Full synchronization
./sync-repos.sh full-sync

# 5. Commit and push both repositories
git add .
git commit -m "Add new feature"
git push

# Then in English repository:
cd ../post-trading-en
git add .
git commit -m "Sync new feature from Czech repo"
git push
```

## Quick Reference Commands

### Synchronization Commands
```bash
# Sync common files only
./sync-repos.sh sync-common

# Update English version with Czech changes
./sync-repos.sh update-en

# Full synchronization (with backup)
./sync-repos.sh full-sync

# Create backup of both repositories
./sync-repos.sh backup

# Validate repository structure
./sync-repos.sh validate
```

### Git Commands
```bash
# Czech repository
git add .
git commit -m "Your commit message"
git push

# English repository
cd ../post-trading-en
git add .
git commit -m "Sync from Czech repo"
git push
```

## Common Scenarios

### Scenario 1: Update CSS Styles
```bash
# 1. Edit styles.css in Czech repo
# 2. Sync to English repo
./sync-repos.sh sync-common
# 3. Commit both repos
```

### Scenario 2: Add New Service
```bash
# 1. Edit Czech content in index.html
# 2. Edit English content in en/index.html
# 3. Update English repo
./sync-repos.sh update-en
# 4. Commit both repos
```

### Scenario 3: Update Contact Information
```bash
# 1. Edit contact info in both index.html files
# 2. Update English repo
./sync-repos.sh update-en
# 3. Commit both repos
```

### Scenario 4: Add New Asset (Image, PDF)
```bash
# 1. Add asset to assets/ folder in Czech repo
# 2. Sync to English repo
./sync-repos.sh sync-common
# 3. Commit both repos
```

## Best Practices

### 1. **Always Test Locally**
- Test both Czech and English versions before pushing
- Check language switching works correctly
- Verify all assets load properly

### 2. **Use Descriptive Commit Messages**
```bash
git commit -m "Add new service: SPV accounting"
git commit -m "Update contact information"
git commit -m "Fix mobile menu styling"
```

### 3. **Keep Repositories in Sync**
- Always run sync commands after making changes
- Don't edit files directly in English repository
- Use Czech repository as the source of truth

### 4. **Backup Before Major Changes**
```bash
./sync-repos.sh backup
```

## Troubleshooting

### Issue: English site shows old content
**Solution:**
```bash
./sync-repos.sh update-en
cd ../post-trading-en
git add .
git commit -m "Force sync from Czech repo"
git push
```

### Issue: Assets not loading on English site
**Solution:**
```bash
./sync-repos.sh sync-common
cd ../post-trading-en
git add .
git commit -m "Sync assets from Czech repo"
git push
```

### Issue: Language switching not working
**Check:**
1. Verify domain URLs in HTML files
2. Check if both sites are accessible
3. Test language detection in config.js

## Deployment

Both repositories automatically deploy to GitHub Pages when you push to the main branch:

- **Czech**: `uctujtrading.cz`
- **English**: `post-trading.com`

No manual deployment needed - GitHub Actions handles it automatically.

## Quick Start Checklist

When making changes:

1. ✅ Edit files in Czech repository
2. ✅ Run appropriate sync command
3. ✅ Test both versions locally
4. ✅ Commit and push Czech repository
5. ✅ Commit and push English repository
6. ✅ Verify both sites work correctly

This workflow ensures both repositories stay in sync and your changes are deployed to both domains automatically!

