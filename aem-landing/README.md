# The Frontier Mindset Lab: AEM landing page
An AEM Edge Delivery Services project, started from [adobe/aem-boilerplate](https://github.com/adobe/aem-boilerplate), with the Lab's visual identity applied.

## Environments
- Preview: https://main--{repo}--{owner}.aem.page/
- Live: https://main--{repo}--{owner}.aem.live/

## Documentation

Before using the aem-boilerplate, we recommend you to go through the documentation on https://www.aem.live/docs/ and more specifically:
1. [Developer Tutorial](https://www.aem.live/developer/tutorial)
2. [The Anatomy of a Project](https://www.aem.live/developer/anatomy-of-a-project)
3. [Web Performance](https://www.aem.live/developer/keeping-it-100)
4. [Markup, Sections, Blocks, and Auto Blocking](https://www.aem.live/developer/markup-sections-blocks)

## Installation

```sh
npm i
```

## Linting

```sh
npm run lint
```

## Local drafts (no AEM license or content source needed)

Pages live as HTML files in `drafts/` and are served by the AEM CLI:

```sh
npx -y @adobe/aem-cli up --html-folder drafts
```

Then open http://localhost:3000/drafts/landing.

- `drafts/landing.plain.html`: the landing page
- `drafts/nav.plain.html`, `drafts/footer.plain.html`: header and footer, wired up through the page's `metadata` block
- Section styles (`lavender`, `peach`, `soft`, `lead`, `gradient-heading`) go directly on the section `<div class="...">`. In a real Google Doc, Word file or da.live document you'd set them as **Style** in a Section Metadata table instead.
- A short all-bold paragraph directly above a heading becomes an eyebrow label.

`aem up` must run from the root of a git repository with an `origin` remote.

## Local development (with a connected content source)

1. Create a new repository based on the `aem-boilerplate` template
1. Add the [AEM Code Sync GitHub App](https://github.com/apps/aem-code-sync) to the repository
1. Install the [AEM CLI](https://github.com/adobe/helix-cli): `npm install -g @adobe/aem-cli`
1. Start AEM Proxy: `aem up` (opens your browser at `http://localhost:3000`)
1. Open the `{repo}` directory in your favorite IDE and start coding :)
