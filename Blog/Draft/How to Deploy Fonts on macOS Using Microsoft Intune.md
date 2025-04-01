## Introduction

Managing fonts in corporate Mac environments can be challenging. Microsoft Intune allows IT admins to remotely deploy fonts without requiring manual installation. In this post, we’ll walk through how to install fonts on macOS via Intune using a shell script.

## Why Deploy Fonts via Intune?

- **Standardized Font Usage** – Ensure all Mac devices in your organization use the same fonts.
- **Automation & Compliance** – Automate font deployment without requiring user interaction.
- **Remote Management** – Deploy fonts across multiple devices from Microsoft Intune.

## Prerequisites

Before proceeding, ensure you have:

- macOS devices **enrolled in Intune**.
- Admin access to **Microsoft Intune**.

## Step 1: Prepare the Deployment Script

This guide can be used to deploy **any fonts**, but for this example, we’ll be deploying **Roboto**.

Use the following shell script to download and install Roboto fonts in `/Library/Fonts` (making them available to all users).

```Shell
#!/bin/bash

# Define the system-wide font directory
FONT_DIR="/Library/Fonts"
mkdir -p "$FONT_DIR"

# Base URL for Google Fonts' GitHub repo
BASE_URL="https://github.com/google/fonts/raw/main/ofl/roboto/"

# Font filenames
FONT1="Roboto%5Bwdth%2Cwght%5D.ttf"
FONT2="Roboto-Italic%5Bwdth%2Cwght%5D.ttf"

echo "Downloading Roboto Variable Fonts..."

# Download and install fonts with error handling
curl -L --fail --silent --show-error -o "$FONT_DIR/Roboto[wdth,wght].ttf" "${BASE_URL}${FONT1}" || { echo "Failed to download Roboto.ttf"; exit 1; }
curl -L --fail --silent --show-error -o "$FONT_DIR/Roboto-Italic[wdth,wght].ttf" "${BASE_URL}${FONT2}" || { echo "Failed to download Roboto-Italic.ttf"; exit 1; }

echo "Roboto Variable Fonts installed successfully in $FONT_DIR"

exit 0
```

## Step 2: Upload the Script to Microsoft Intune

1. **Go to Microsoft Intune**
    - Navigate to **Devices** > **macOS** > **Shell Scripts**
    - Click **+ Add**
2. **Upload the script**
    - Name: **Install Roboto Fonts**
    - Description: **Deploys Roboto fonts to macOS devices using Intune**
    - **Upload the script (**`**install_roboto_fonts.sh**`**)**
3. **Configure Execution Settings**
    - **Run script as signed-in user:** ❌ No
    - **Hide script notifications:** ✅ Yes (optional)
    - **Script frequency:** ⏳ Once
    - **Script timeout:** 30 minutes (default)
4. **Assign to Target Mac Devices**
    - Assign to a **test group** first.
    - Deploy to **production devices** once tested.

## Step 3: Verify Installation

Once deployed, confirm the fonts are installed:

🔹 Open **Finder** and navigate to `/Library/Fonts`.

🔹 Verify that **Roboto[wdth,wght].ttf** and **Roboto-Italic[wdth,wght].ttf** exist.

🔹 Open an app like **Pages or Keynote** and check if **Roboto appears in the font list**.

## Troubleshooting & Logs

If the fonts don’t install, check logs using:

```Shell
cat /var/log/install.log | grep "Roboto"
```

Or check **Intune logs on macOS**:

```Shell
cat /Library/Logs/Microsoft/Intune/IntuneMDMDaemon.log
```

## Conclusion

By using **Microsoft Intune**, you can automate font deployment across your macOS devices, ensuring consistency and reducing manual work for IT admins. This approach can be adapted to deploy **any other fonts** required by your organization.