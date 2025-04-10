### 1. YAML Data File

You define all affiliate links in a single, central file:  
`/data/affiliatelinks.yaml`

```yaml
surfer_seo:
  url: "https://partner.com/surfer"
  label: "Surfer SEO"
  campaign: "ai-tools"

jasper_ai:
  url: "https://partner.com/jasper"
  label: "Jasper AI"
  campaign: "ai-tools"

vidnoz:
  url: "https://partner.com/vidnoz"
  label: "Vidnoz AI"
  campaign: "video-tools"

```
Each entry includes the affiliate URL, label, and campaign for UTM tracking.

### 2. Shortcode for Buttons

You created this shortcode at:  
`layouts/shortcodes/affiliate-button.html`

```html
{{ $key := .Get "id" }}
{{ $link := index site.Data.affiliatelinks $key }}

{{ if $link }}
  <div style="text-align: center; margin: 2em 0;">
    <a 
      class="affiliate-button"
      href="{{ $link.url }}?utm_source=kjetilfuras.com&utm_medium=affiliate&utm_campaign={{ $link.campaign }}"
      target="_blank"
      rel="nofollow sponsored noopener"
      data-ga-category="Affiliate"
      data-ga-label="{{ $link.label }}"
    >
      {{ $link.label }}
    </a>
  </div>
{{ else }}
  <p style="color: red; font-weight: bold;">Affiliate link ID "{{ $key }}" not found.</p>
{{ end }}

```
This dynamically builds a trackable, styled CTA button with full UTM support and Google Analytics data attributes.

### 3. Using the Shortcode in Markdown

You drop buttons in your blog posts like this:

```markdown
{{< affiliate-button id="surfer_seo" >}}
{{< affiliate-button id="jasper_ai" >}}
```

### 4. Custom Button Styling

In your `assets/css/custom.css`:

```css
.affiliate-button {
  display: inline-block;
  background-color: #007acc;
  color: white;
  padding: 0.6em 1.2em;
  border-radius: 5px;
  text-decoration: none;
  font-weight: 600;
  transition: background-color 0.2s ease;
}

.affiliate-button:hover {
  background-color: #005f99;
}
```
