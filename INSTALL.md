# Installation Guide

## Install from GitHub

You can install hookbuster directly from GitHub using npm:

### Global Installation (Recommended)

Install globally to use the `hookbuster` command from anywhere:

```bash
npm install -g git+https://github.com/jingkunhuang/hookbuster.git
```

After installation, you can run hookbuster using:

```bash
hookbuster
```

Or with the full node command:

```bash
npx hookbuster
```

### Local Installation

Install as a dependency in your project:

```bash
npm install git+https://github.com/jingkunhuang/hookbuster.git
```

Then run it using:

```bash
npx hookbuster
```

Or add it to your `package.json` scripts:

```json
{
  "scripts": {
    "hookbuster": "hookbuster"
  }
}
```

### Install Specific Version/Branch/Tag

Install a specific version:

```bash
npm install git+https://github.com/jingkunhuang/hookbuster.git#v1.0.0
```

Install from a specific branch:

```bash
npm install git+https://github.com/jingkunhuang/hookbuster.git#main
```

Install from a specific commit:

```bash
npm install git+https://github.com/jingkunhuang/hookbuster.git#abc1234
```

## Install from Cloned Repository

If you've already cloned the repository:

```bash
# Clone the repository
git clone https://github.com/jingkunhuang/hookbuster.git
cd hookbuster

# Install dependencies
npm install

# Run the application
node app.js
```

Or install globally from the cloned directory:

```bash
npm install -g .
```

## Verify Installation

Check that hookbuster is installed correctly:

```bash
# Check version
npm list -g hookbuster

# Test the command
hookbuster --help
```

## Uninstall

Global uninstall:

```bash
npm uninstall -g hookbuster
```

Local uninstall:

```bash
npm uninstall hookbuster
```

## Troubleshooting

### Permission Errors (EACCES)

If you get permission errors on macOS/Linux, either:

1. Use `sudo` (not recommended):
   ```bash
   sudo npm install -g git+https://github.com/jingkunhuang/hookbuster.git
   ```

2. Configure npm to use a different directory (recommended):
   ```bash
   mkdir ~/.npm-global
   npm config set prefix '~/.npm-global'
   echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
   source ~/.bashrc
   ```

### Git Not Found

Ensure Git is installed and accessible:

```bash
git --version
```

If not installed, visit: https://git-scm.com/downloads

### SSH vs HTTPS

If you have SSH keys configured with GitHub, you can use SSH:

```bash
npm install -g git+ssh://git@github.com/jingkunhuang/hookbuster.git
```

For HTTPS (no authentication required for public repos):

```bash
npm install -g git+https://github.com/jingkunhuang/hookbuster.git
```

## Usage After Installation

Once installed, refer to the main [README.md](README.md) for usage instructions.

Quick start:

```bash
# Interactive mode
hookbuster

# With environment variables
export TOKEN="your_webex_token"
export PORT="5000"
hookbuster
```
