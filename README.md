# GitHub Actions – Next.js Build with Caching & Artifacts 🚀

This workflow automates the **build process** for your Next.js application and uploads the built files as **artifacts**. It also uses **caching** to speed up dependency installation on subsequent runs.  

---

## 🔑 Key Features

1. **Automatic build on push** – Runs whenever code is pushed to the `main` branch.  
2. **Node.js environment setup** – Configures Node.js and caches `npm` dependencies.  
3. **Build the Next.js app** – Runs `npm run build`.  
4. **Upload build artifacts** – Saves the output folder (`out/`) so it can be downloaded later or used in other workflows.  

---

## 📂 Workflow File

```yaml
name: Next JS Build with Caching & Artifacts

on:
  push:
    branches: [ main ]  # Trigger workflow on pushes to main branch

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # Step 1: Checkout repository
      - name: Checkout Repository
        uses: actions/checkout@v4.2.2

      # Step 2: Setup Node.js environment with caching
      - name: Setup Node JS
        uses: actions/setup-node@v4.2.0
        with:
          node-version: 22.x
          cache: 'npm'

      # Step 3: Install dependencies
      - name: Install Dependencies
        run: npm install

      # Step 4: Build Next.js app
      - name: Build Next Js App
        run: npm run build

      # Step 5: Upload build artifacts
      - name: Upload Build on Artifacts
        uses: actions/upload-artifact@v4.6.0
        with:
          name: nextjs-build
          path: out/   # Directory containing the built app


🔹 How it Works

Checkout Repository – Pulls your code into the runner.

Setup Node.js – Installs Node.js version 22.x and enables caching for npm dependencies to speed up future runs.

Install Dependencies – Installs all Node.js packages listed in package.json.

Build Next.js App – Runs npm run build, which creates a production-ready build.

Upload Artifacts – The out/ folder is uploaded as a workflow artifact. You can download it from the workflow run page or use it in subsequent workflows like deployments.




⚡ Benefits

Faster builds thanks to dependency caching.

Safe storage of build artifacts for deployment pipelines.

Automated workflow ensures builds are consistent and reproducible.
