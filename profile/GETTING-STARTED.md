# 🚀 Getting Started

Welcome to the SurePayroll GitHub organization! Before you can contribute, you'll need to complete the following setup requirements.

---

## ✅ Requirements Checklist

- [ ] 📧 Link your Paychex email to GitHub
- [ ] 🔐 Enable non-SMS two-factor authentication
- [ ] 🔏 Set up GPG commit signing
- [ ] 🖼️ Set up a picture for your github profile (preferrably same as your paychex picture)

---

## 1. 📧 Link Your Paychex Email

Your `@paychex.com` email address must be linked to your GitHub account.

### How to Link Your Email

1. Go to **[GitHub Email Settings](https://github.com/settings/emails)**
2. Under **Add email address**, enter your `@paychex.com` email
3. Click **Add**
4. Check your Paychex inbox for a verification email from GitHub
5. Click the verification link to confirm

> 💡 **Tip**: You can keep your personal email as your primary email, but your Paychex email must be added and verified.

📚 **GitHub Docs**: [Adding an email address to your GitHub account](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/adding-an-email-address-to-your-github-account)

---

## 2. 🔐 Enable Non-SMS Two-Factor Authentication

SMS-based 2FA is vulnerable to SIM-swapping attacks. You must use a more secure 2FA method.

### ✅ Approved 2FA Methods

| Method | Examples |
|--------|----------|
| 📱 **Authenticator app** (recommended) | 1Password, Authy, Google Authenticator, Microsoft Authenticator |
| 🔑 **Security key** | YubiKey, Titan Security Key |
| 🖐️ **Passkey** | Device-based biometric authentication |

### How to Set Up 2FA

1. Go to **[GitHub Password and Authentication Settings](https://github.com/settings/security)**
2. Click **Enable two-factor authentication**
3. Choose **Authenticator app** or **Security key** (⚠️ do NOT choose SMS)
4. Follow the on-screen instructions to complete setup
5. **Save your recovery codes** in a secure location (1Password recommended)

### ⚠️ If You Currently Use SMS 2FA

1. Go to **[GitHub Password and Authentication Settings](https://github.com/settings/security)**
2. Under **Two-factor methods**, add an authenticator app or security key
3. Once added, remove SMS as a 2FA method

📚 **GitHub Docs**: [Configuring two-factor authentication](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication)

---

## 3. 🔏 Set Up GPG Commit Signing

All commits must be GPG-signed to verify they actually came from you. Unsigned commits will be rejected.

### Step 1: Install GPG

#### 🍎 macOS

```bash
# Install GPG using Homebrew
brew install gnupg

# Verify installation
gpg --version
```

> 💡 **Don't have Homebrew?** Get it at [brew.sh](https://brew.sh)

#### 🪟 Windows

Download and install [Gpg4win](https://www.gpg4win.org/)

#### 🐧 Linux

```bash
# Debian/Ubuntu
sudo apt-get install gnupg

# Fedora
sudo dnf install gnupg2
```

### Step 2: Generate a GPG Key

```bash
# Generate a new GPG key
gpg --full-generate-key
```

When prompted, use these settings:
- **Key type**: RSA and RSA (default)
- **Key size**: `4096`
- **Expiration**: `1y` (recommended) or `0` for no expiration
- **Real name**: Your full name
- **Email**: `your.name@paychex.com` ⚠️ Must match your Paychex email!

### Step 3: Get Your GPG Key ID

```bash
# List your GPG keys
gpg --list-secret-keys --keyid-format=long
```

Output will look like:
```
sec   rsa4096/ABC123DEF456GH78 2024-01-01 [SC]
      1234567890ABCDEF1234567890ABCDEF12345678
uid                 [ultimate] Your Name <your.name@paychex.com>
```

📝 The key ID is the part after `rsa4096/` (e.g., `ABC123DEF456GH78`)

### Step 4: Add Your GPG Key to GitHub

```bash
# Export your public key (replace KEY_ID with your actual key ID)
gpg --armor --export KEY_ID
```

1. Copy the entire output (including `-----BEGIN PGP PUBLIC KEY BLOCK-----` and `-----END PGP PUBLIC KEY BLOCK-----`)
2. Go to **[GitHub SSH and GPG Keys Settings](https://github.com/settings/keys)**
3. Click **New GPG key**
4. Paste your public key and click **Add GPG key**

### Step 5: Configure Git for Signed Commits

```bash
# Set your signing key (replace KEY_ID with your actual key ID)
git config --global user.signingkey KEY_ID

# Enable commit signing by default
git config --global commit.gpgsign true

# Enable tag signing by default
git config --global tag.gpgsign true

# Ensure your Git email matches your GPG key
git config --global user.email "your.name@paychex.com"

# Update the path to match your username and system configuration
echo 'pinentry-program "/usr/bin/pinentry-basic"' >> ~/.gnupg/gpg-agent.conf

git config --global gpg.program "/usr/bin/gpg"

gpgconf --kill gpg-agent
gpgconf --reload gpg-agent
```

#### 🍎 macOS Users: Additional Configuration

Add this to your shell profile (`~/.zshrc` or `~/.bashrc`):

```bash
export GPG_TTY=$(tty)
```

Then reload your shell:

```bash
source ~/.zshrc  # or source ~/.bashrc
```

### Step 6: Verify Your Setup

```bash
# Create a test signed commit
git commit --allow-empty -m "Test signed commit"

# Verify the commit is signed
git log --show-signature -1
```

You should see: `Good signature from "Your Name <your.name@paychex.com>"`

### 🛠️ Troubleshooting

<details>
<summary><strong>❌ "secret key not available" error</strong></summary>

```bash
# Ensure your Git email matches your GPG key email
git config --global user.email "your.name@paychex.com"

# Restart the GPG agent
gpgconf --kill gpg-agent
```
</details>

<details>
<summary><strong>❌ GPG prompt not appearing</strong></summary>

```bash
# Add to your shell profile
export GPG_TTY=$(tty)

# Or use pinentry-mac (macOS)
brew install pinentry-mac
echo "pinentry-program $(which pinentry-mac)" >> ~/.gnupg/gpg-agent.conf
gpgconf --kill gpg-agent
```
</details>

📚 **GitHub Docs**: [Managing commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification)

### Step 5: Set up a picture for your github profile

1. Click your profile photo (top-right corner) → Settings                                                                       
2. Under Profile Picture, click Edit → Upload a photo...                                                                        
3. Select your image, click Upload                                                                                              
4. Crop it and click Set new profile picture                                           

Image requirements:
  - PNG, JPG, or GIF
  - Under 1 MB
  - Max 3000x3000 px (recommended ~500x500 px)

Sources:
  - https://docs.github.com/en/account-and-profile/tutorials/personalize-your-profile
  - https://docs.github.com/en/get-started/start-your-journey/setting-up-your-profile

---

## 🆘 Need Help?

If you encounter issues with any of these steps:

1. 📖 Check the linked GitHub documentation
2. 🔍 Search for your error message online
3. 💬 Reach out to the `@surepayroll/org-admins` team

---

## 🎉 You're All Set!

Once you've completed all the requirements above, you're ready to contribute to SurePayroll repositories. Welcome to the team! 🚀
