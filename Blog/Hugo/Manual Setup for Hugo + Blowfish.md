
## Step1. Install the Necessary Tools

```bash
  brew install hugo git node
```

## Step 2. Create a New Hugo Site

Initialize a new Hugo project:

```bash
hugo new site ~/code/blog
```

## Step 3. Install the Blowfish Theme

Install Blowfish as a Git submodule:

```bash
cd mywebsite
git init
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish

```
## Step 1: Create a New Hugo Site
```bash
hugo new site my-blog cd my-blog
```


> This creates the base directory structure (`content/`, `layouts/`, `static/`, etc.).