
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
cd ~/code/blog
git init
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```

### 3.1. Create Config folders

```bash
mkdir -p config/_default
```

## Step 4. Set Up Theme Configuration Files

### 4.1. Remove the Default Configuration File (Don´t delete yet)

Hugo generates a default `hugo.toml` file in your project's root directory. For Blowfish, it's recommended to delete this file to avoid conflicts:

```bash
rm hugo.toml
```

### 4.2. Copy Blowfish's Example Configuration Files

Blowfish provides example configuration files that you can use as a starting point. Copy these files into your site's `config/_default/` directory:

```bash
cp themes/blowfish/config/_default/* config/_default
```

You should be left with a folder like this:

```bash
config/_default/
├─ hugo.toml
├─ languages.en.toml
├─ markup.toml
├─ menus.en.toml
├─ module.toml  # if you installed using Hugo Modules
└─ params.toml
```

### 4.3. Brung up the website

Head into the `hugo.toml` file and uncomment the line:

```yml
# theme = "blowfish" # UNCOMMENT THIS LINE
```
> This will enable the webserver and you can see changes done in real time.

