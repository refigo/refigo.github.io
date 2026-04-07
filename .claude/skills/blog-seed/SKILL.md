---
name: blog-seed
description: Register a blog seed (file path or URL) into the task system and create a draft blog post. Use when the user provides external content to turn into a blog post.
invocation: user
arguments:
  - name: source
    description: "File path or URL to the blog seed content"
    required: true
---

# Blog Seed → Draft Post Pipeline

You are helping the user turn external content (blog seeds) into draft blog posts for their Astro-based blog at `refigo.github.io`.

## Workflow

### Step 1: Read the seed content

- If `$ARGUMENTS` is a **file path**: read the file using the Read tool.
- If `$ARGUMENTS` is a **URL**: fetch the content using WebFetch.
- Analyze the seed content: identify the title, topic, key points, and language.

### Step 2: Register in the task system

1. Determine a short slug for the post (lowercase, kebab-case, with date suffix like `YYYYMMDD`).
2. Create a task detail file at `docs/tasks/details/content-<slug>.md` with:
   - Summary of the seed content
   - Source path/URL for reference
   - Checklist of remaining work (review, images, translation, etc.)
3. Add an entry to `docs/tasks/IN-PROGRESS.md` under the `## Content` section:
   ```
   - [ ] [<post title>](details/content-<slug>.md) — source: `<path or URL>`
   ```

### Step 3: Create the draft post

1. Create directory: `src/content/post/<slug>/`
2. Create `ko.md` (or appropriate language file) with proper frontmatter:

```yaml
---
title: "<title, max 60 chars>"
description: "<1-2 sentence description>"
publishDate: "<YYYY-MM-DD>"
tags:
  - <relevant tags, lowercase>
draft: true
pinned: false
---
```

3. Adapt the seed content into the post body:
   - Preserve the original content structure and quality.
   - If the seed is already well-written, keep it mostly as-is.
   - Ensure images use relative paths (`./images/`) if applicable.
   - Add proper markdown formatting consistent with existing posts.

### Step 4: Report

Summarize what was created:
- Task detail file path
- Draft post file path
- Any items that need manual attention (missing images, review needed, etc.)

## Important Rules

- Always set `draft: true` — the user will publish manually.
- Title must be 60 characters or fewer (blog schema constraint).
- Tags should be lowercase.
- Respect the existing post structure — look at `src/content/post/` for examples.
- Do NOT auto-publish (set draft to false) without explicit user approval.
