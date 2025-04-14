## 1. Add FAQ Data to Front Matter (`index.md`)

```markdown
faq:
  - question: What is AI marketing software?
    answer: |
      AI marketing software utilizes artificial intelligence technologies to automate decision-making, analyze data, and improve marketing efforts.

      By leveraging machine learning and data analysis, businesses can enhance engagement and boost marketing efficiency.
  - question: What is the best tool for AI in marketing?
    answer: There’s no one-size-fits-all. Tools like Jasper, Surfer SEO, and Grammarly offer different strengths depending on your needs.

```

## 2. Add a Markdown TOC Heading (for visibility)

At the **end of your Markdown file**, add:

```markdown
## Frequently Asked Questions
```
> This makes the FAQ section appear in Hugo’s `.TableOfContents`.

## 3. Render FAQs Visually with a Partial

Create this file:  `layouts/partials/article/faq-content.html`

```html
{{ with .Params.faq }}
<section class="mt-4" id="frequently-asked-questions">
  <div class="space-y-4">
    {{ range . }}
    <details
      class="border p-4 rounded-lg transition duration-200 ease-in-out hover:shadow-md focus:outline-none focus:ring-0 focus:outline-offset-0"
    >
      <summary class="cursor-pointer font-medium text-neutral-800 dark:text-neutral-100">
        {{ .question }}
      </summary>
      <p class="mt-2 text-neutral-700 dark:text-neutral-300">{{ .answer | markdownify }}</p>
    </details>
    {{ end }}
  </div>
</section>
{{ end }}

```
Then include it in `single.html` or your post template **below `.Content`**:

```html
{{ partial "article/faq-content.html" . }}
```