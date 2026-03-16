# Changelog

All notable changes to this project will be documented in this file.

## [1.0.0] - 2026-03-16

### Added
- **NPM GitHub Installation Support**: Package now supports direct installation from GitHub
  - Added proper `package.json` metadata (version, description, repository, author)
  - Added `bin` configuration to enable global CLI installation
  - Added `homepage` and `bugs` URLs for better discoverability
  - Added `engines` field to specify minimum Node.js version (>=14.0.0)
  - Added keywords for better searchability
  - Added `start` script for convenience

- **CLI Executable**: Added shebang (`#!/usr/bin/env node`) to `app.js` to make it work as a CLI tool

- **Documentation**:
  - Created `INSTALL.md` with comprehensive installation instructions
  - Created `.npmignore` to exclude development files from npm package
  - Updated `README.md` with GitHub installation instructions
  - Created `CHANGELOG.md` to track version history

### Changed
- Updated `package.json`:
  - Version: "" → "1.0.0"
  - Description: Added detailed description
  - Main: "index.js" → "app.js" (correct entry point)
  - Author: "" → "Jingkun Huang"
  - Added repository information pointing to https://github.com/jingkunhuang/hookbuster.git

- Updated `README.md`:
  - Added GitHub installation as the primary installation method
  - Added reference to INSTALL.md for detailed instructions

### Installation Methods

Users can now install hookbuster using any of these methods:

1. **Global installation from GitHub**:
   ```bash
   npm install -g git+https://github.com/jingkunhuang/hookbuster.git
   hookbuster
   ```

2. **Local installation from GitHub**:
   ```bash
   npm install git+https://github.com/jingkunhuang/hookbuster.git
   npx hookbuster
   ```

3. **Clone and install**:
   ```bash
   git clone https://github.com/jingkunhuang/hookbuster.git
   cd hookbuster
   npm install
   node app.js
   ```

### Technical Details

- Package size: 13.7 kB (optimized with `.npmignore`)
- Total files in package: 9 essential files
- Node.js compatibility: >=14.0.0
- Binary command: `hookbuster`
