While experimenting on my Mac i accidentally wiped my $PATH.

### 1. **Ensure Rancher Desktop CLI tools are enabled**

First I factory reset mu Rancher Desktop installation

### 2. Manually check where Rancher installs them

Ran this to see if it installed Rancher’s CLI wrappers:

```bash
ls -l /usr/local/bin/docker
ls -l /usr/local/bin/kubectl
```
Which it didn't

You should see something like:

```bash
/usr/local/bin/docker -> /Applications/Rancher Desktop.app/Contents/Resources/resources/darwin/bin/docker
```

### 3. **Manually add Rancher’s binaries to your PATH**

Find where Rancher Desktop stores its CLI tools:

```bash
ls "/Applications/Rancher Desktop.app/Contents/Resources/resources/darwin/bin/"
```
You should see `docker`, `kubectl`, and other tools in there.

If yes, add this to your `~/.zshrc` (top of file):