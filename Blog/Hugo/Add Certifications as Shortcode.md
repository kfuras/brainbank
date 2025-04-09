#### 1. Create a Shortcode File

Create a file in your Hugo project:

```bash
layouts/shortcodes/certifications.html
```

> If it doesn't exist, create the `shortcodes/` folder inside `layouts/`.

#### 2. Paste the HTML in That File

Paste this in `certifications.html`:
```html
<div class="certifications-container">
    <div class="certification">
      <a href="https://learn.microsoft.com/api/credentials/share/en-us/KjetilFurs-3628/3DC41FBA975DE8C4?sharingId=E735EEC265D912D0" target="_blank" rel="noopener noreferrer">
        <img src="https://learn.microsoft.com/media/learn/certification/badges/microsoft-certified-associate-badge.svg" alt="Microsoft Certified: Azure Administrator Associate">
        <p>Microsoft Certified: Azure Administrator Associate</p>
      </a>
    </div>
    <div class="certification">
      <a href="https://learn.microsoft.com/api/credentials/share/en-us/KjetilFurs-3628/4491891F35838FE6?sharingId=E735EEC265D912D0" target="_blank" rel="noopener noreferrer">
        <img src="https://learn.microsoft.com/media/learn/certification/badges/microsoft-certified-expert-badge.svg" alt="Microsoft Certified: Azure Solutions Architect Expert">
        <p>Microsoft Certified: Azure Solutions Architect Expert</p>
      </a>
    </div>
  </div>
  ```

### 3. Add the CSS

Create a file:  
`assets/css/custom.css`  
(if it doesn't exist yet)

Then paste your CSS:

```css
.certifications-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: flex-start;
    margin-top: 2rem;
}

.certification {
    text-align: center;
    margin: 10px;
    flex-basis: 20%;
}

.certification img {
    width: 100px;
    height: auto;
    display: block;
    margin: 0 auto;
}

.certification p {
    margin-top: 10px;
    color: #ffffff;
    font-size: 16px;
}

@media (max-width: 768px) {
    .certifications-container {
        justify-content: center;
    }

    .certification {
        flex-basis: 90%;
        margin: 10px 5%;
    }

    .certification img {
        width: 80px;
    }

    .certification p {
        font-size: 14px;
    }
}

```

### 3. Load Your CSS in `config.toml`

If you're using TOML:

```toml
customCSS = ["css/custom.css"]
```

If you're using YAML:

```yaml
params:
  customCSS:
    - css/custom.css

```

### 4. Use It Inside Your Markdown

Now, in any Markdown page, you can just write:

```markdown
{{< certifications >}}
```

…and it will render your entire badge block.