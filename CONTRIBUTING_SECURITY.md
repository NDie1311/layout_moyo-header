# Secure Development Guidelines

## Purpose

This document provides security guidelines for contributors to this project to ensure the repository remains secure and doesn't expose sensitive information.

## General Security Principles

### 1. Never Commit Sensitive Information

**Never** commit any of the following to the repository:

- Passwords or password hashes
- API keys or tokens
- Private SSH keys
- SSL/TLS certificates or private keys
- Database credentials
- Cloud service credentials (AWS, Azure, GCP keys)
- Personal Identifiable Information (PII)
- Credit card or banking information
- Internal URLs or IP addresses
- Email addresses (except in LICENSE or SECURITY.md)

### 2. Use Environment Variables

For any configuration that varies between environments or contains sensitive data:

```javascript
// ❌ WRONG - Never hardcode credentials
const apiKey = "sk_live_123456789abcdef";

// ✅ CORRECT - Use environment variables
const apiKey = process.env.API_KEY;
```

### 3. Review Changes Before Committing

Before every commit:

```bash
# Review what you're about to commit
git status
git diff

# Check for sensitive patterns
git diff | grep -iE '(password|secret|key|token|api_key|credential)'
```

### 4. Use .gitignore Properly

The `.gitignore` file is configured to exclude common sensitive files. Always:

- Review `.gitignore` before adding new file types
- Never use `git add -f` to force-add ignored files (unless you're absolutely sure)
- Test that sensitive files are actually ignored

### 5. Dependencies Security

Keep dependencies secure:

```bash
# Check for vulnerabilities
npm audit

# Fix vulnerabilities automatically where possible
npm audit fix

# Check for outdated packages
npm outdated

# Update packages
npm update
```

### 6. Code Review Checklist

When reviewing code, check for:

- [ ] No hardcoded credentials or secrets
- [ ] No commented-out sensitive information
- [ ] Proper use of environment variables
- [ ] No unnecessary permissions or access
- [ ] Input validation and sanitization (if applicable)
- [ ] No exposure of internal system details
- [ ] Dependencies are up-to-date and secure

## GitHub-Specific Security

### 1. Personal Access Tokens

If you need to create a Personal Access Token:

- Grant minimal permissions (principle of least privilege)
- Set an expiration date
- Use fine-grained tokens when possible
- Store tokens securely (never commit them)
- Rotate tokens regularly
- Delete tokens you no longer use

### 2. GitHub Secrets

For CI/CD workflows, use GitHub Secrets:

```yaml
# In GitHub Actions workflow
- name: Deploy
  env:
    API_KEY: ${{ secrets.API_KEY }}
  run: ./deploy.sh
```

### 3. Repository Settings

Recommended repository security settings:

- Enable "Require pull request reviews before merging"
- Enable "Require status checks to pass before merging"
- Enable branch protection on `master` and `develop`
- Enable "Dependabot alerts"
- Enable "Dependabot security updates"
- Enable "Secret scanning" (if available)

## If You Accidentally Commit Sensitive Data

If you accidentally commit sensitive information:

### 1. Immediate Actions

1. **Invalidate the compromised credentials immediately**
   - Revoke API keys
   - Change passwords
   - Rotate tokens
   - Generate new keys

2. **Notify the team**
   - Alert maintainers immediately
   - Document what was exposed and when

### 2. Remove from Git History

For recent commits not yet pushed:

```bash
# Reset to before the commit
git reset --soft HEAD~1
git reset HEAD <file-with-secrets>
```

For commits already pushed, you need to rewrite history (requires force push):

```bash
# Use git filter-repo (recommended)
git filter-repo --path <file-with-secrets> --invert-paths

# Or use BFG Repo-Cleaner
bfg --delete-files <file-with-secrets>
```

**Warning**: Rewriting history affects all contributors and should be coordinated.

### 3. Alternative: Make Repository Private

If sensitive data is extensively exposed:

1. Make the repository private immediately
2. Create a new repository without the sensitive history
3. Migrate the clean code to the new repository

## Security Tools

### Recommended Tools for Local Development

1. **git-secrets** - Prevents committing secrets
   ```bash
   git secrets --install
   git secrets --register-aws
   ```

2. **Gitleaks** - Scan for secrets in repository
   ```bash
   gitleaks detect --source . --verbose
   ```

3. **npm audit** - Check for vulnerable dependencies
   ```bash
   npm audit
   ```

### IDE/Editor Plugins

- **VS Code**: GitLens, Security Scanner
- **IntelliJ/WebStorm**: CheckStyle, Security Scan
- **Sublime Text**: GitGutter, SublimeLinter

## Secure Coding Practices for This Project

Since this is a frontend layout project with HTML/CSS:

### 1. External Resources

When linking external resources:

```html
<!-- ✅ GOOD - Use integrity checks for CDN resources -->
<link 
  rel="stylesheet" 
  href="https://cdn.example.com/style.css"
  integrity="sha384-..."
  crossorigin="anonymous"
>

<!-- ✅ GOOD - Use HTTPS only -->
<link rel="stylesheet" href="https://fonts.googleapis.com/...">

<!-- ❌ BAD - Avoid HTTP -->
<link rel="stylesheet" href="http://unsecure-site.com/style.css">
```

### 2. HTML Comments

```html
<!-- ❌ WRONG - Don't leave sensitive info in comments -->
<!-- TODO: Remove this before production. API key: abc123 -->

<!-- ✅ CORRECT - Keep comments generic -->
<!-- TODO: Implement user authentication -->
```

### 3. Asset Files

- Don't commit large binary files unless necessary
- Optimize images before committing
- Use Git LFS for large assets if needed
- Never commit compiled/build artifacts

## Questions?

If you have questions about security practices:

1. Check the [SECURITY.md](SECURITY.md) file
2. Consult GitHub's [Security Best Practices](https://docs.github.com/en/code-security)
3. Ask in pull request reviews
4. Contact repository maintainers

## Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [GitHub Security Best Practices](https://docs.github.com/en/code-security)
- [npm Security Best Practices](https://docs.npmjs.com/security-best-practices)
- [Git Secrets Tools](https://github.com/awslabs/git-secrets)
