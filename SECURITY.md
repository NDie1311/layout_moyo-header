# Security Policy

## Reporting a Security Vulnerability

If you discover a security vulnerability in this project, please report it by creating a private security advisory on GitHub or by contacting the repository maintainer directly.

## GitHub Account Security Best Practices

If you believe your GitHub account has been compromised or your financial information has been stolen, follow these immediate steps:

### Immediate Actions

1. **Change your GitHub password immediately**
   - Go to GitHub Settings → Password and Security
   - Use a strong, unique password (at least 16 characters with uppercase, lowercase, numbers, and symbols)
   - Use a password manager to generate and store secure passwords

2. **Enable Two-Factor Authentication (2FA)**
   - Go to GitHub Settings → Password and Security → Two-factor authentication
   - Use an authenticator app (Google Authenticator, Authy, or Microsoft Authenticator)
   - Save your recovery codes in a secure location
   - **This is critical** - 2FA prevents unauthorized access even if your password is compromised

3. **Review your GitHub account access**
   - Go to Settings → Applications → Authorized OAuth Apps
   - Revoke access to any applications you don't recognize or no longer use
   - Go to Settings → Applications → Installed GitHub Apps
   - Review and remove any suspicious GitHub Apps

4. **Check your SSH and GPG keys**
   - Go to Settings → SSH and GPG keys
   - Remove any SSH keys you don't recognize
   - Remove any GPG keys you don't recognize

5. **Review your Personal Access Tokens**
   - Go to Settings → Developer settings → Personal access tokens
   - Delete any tokens you don't recognize or no longer need
   - Regenerate necessary tokens with minimal permissions

6. **Check your connected accounts**
   - Go to Settings → Account security → Sessions
   - Review active sessions and revoke any you don't recognize

7. **Review your account activity**
   - Go to Settings → Security log
   - Review recent activities for any suspicious actions
   - Look for unauthorized commits, repository access, or setting changes

### Bank and Financial Security

If your bank card details were compromised:

1. **Contact your bank immediately**
   - Report the fraudulent charges
   - Request a new card with a new number
   - Set up fraud alerts on your account

2. **Review all your online accounts**
   - Change passwords on all accounts where you used the same password
   - Enable 2FA on all accounts that support it (especially email, banking, and social media)

3. **Monitor your credit**
   - Check your credit report for unauthorized accounts
   - Consider a credit freeze or fraud alert

### Important Notes

**About this Repository**: This is a frontend HTML/CSS layout project with no backend functionality, no payment processing, and no collection of user data. If your financial information was compromised, it is **not** related to this specific repository's code.

**Possible causes of compromise:**
- Phishing emails or websites impersonating GitHub
- Malware or keyloggers on your computer
- Reused passwords from other breached services
- Unsecured WiFi networks
- Social engineering attacks
- Compromised browser extensions

### Prevention for the Future

1. **Never share your credentials**
   - Don't commit passwords, API keys, or tokens to repositories
   - Use environment variables for sensitive data
   - Use GitHub Secrets for CI/CD workflows

2. **Use a password manager**
   - Generate unique, strong passwords for every service
   - Popular options: 1Password, Bitwarden, LastPass

3. **Keep your computer secure**
   - Use antivirus software and keep it updated
   - Keep your operating system and applications updated
   - Don't install software from untrusted sources

4. **Be cautious of phishing**
   - Always verify the URL before entering credentials
   - GitHub's official domain is `github.com` (check the address bar carefully)
   - GitHub will never ask for your password via email

5. **Use secure networks**
   - Avoid public WiFi for sensitive operations
   - Use a VPN when on untrusted networks

## Repository Security Best Practices

For contributors to this repository:

1. **Never commit sensitive information**
   - No passwords, API keys, tokens, or credentials
   - Use `.gitignore` to exclude sensitive files
   - Review commits before pushing

2. **Keep dependencies updated**
   - Regularly update npm packages to patch security vulnerabilities
   - Monitor GitHub security alerts

3. **Code review**
   - Review all code changes for security issues
   - Watch for malicious code or suspicious patterns

## Resources

- [GitHub Security Documentation](https://docs.github.com/en/code-security)
- [GitHub Account Security](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure)
- [Two-Factor Authentication Setup](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa)
- [Removing Sensitive Data from a Repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
