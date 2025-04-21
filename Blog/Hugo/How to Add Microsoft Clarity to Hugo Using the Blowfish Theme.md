1. Get Your Clarity Tracking Code**
	- Go to [clarity.microsoft.com](https://clarity.microsoft.com) and create a new project.
    - Copy the JavaScript snippet provided (you’ll paste this later).
2. **Create a `head-include.html` Partial in Your Project**
    - In your Hugo site folder (not the theme folder), create this file:

```bash
layouts/partials/head-include.html
```

Paste your Clarity tracking script into that file.  
Example:

```html
<script type="text/javascript"> (function(c,l,a,r,i,t,y){ c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)}; t=l.createElement(r);t.async=1;t.src="https://www.clarity.ms/tag/"+i; y=l.getElementsByTagName(r)[0];y.parentNode.insertBefore(t,y); })(window, document, "clarity", "script", "YOUR_PROJECT_ID"); </script>
```

3. **Enable the Partial in Your Head**
	- Blowfish does not include `head-include.html` by default, so copy the theme’s `head.html` to your project:

```bash
mkdir -p layouts/partials/
cp themes/blowfish/layouts/partials/head.html layouts/partials/

```

Edit your copied `layouts/partials/head.html` and **add this line at the very end**, just before `</head>`.
Example:

```html
{{ partial "head-includes.html" . }}
</head>
```

4. **Rebuild and Deploy Your Site**
    - Run `hugo` and redeploy your site so the changes take effect.
    
5. **Visit and Test**
    - Open your site in a regular browser window (not incognito or with adblock).
    - Click around and wait 10–30 minutes. Clarity will begin showing recordings under the **Recordings** tab.