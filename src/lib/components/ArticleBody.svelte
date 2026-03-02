<!--
@component
ArticleBody.svelte — NYCity News Service Style Article Content

A wrapper component that provides proper typography for article body text.
Uses sans-serif font for body, serif for subheadings.

USAGE EXAMPLE:
<ArticleBody>
  <p>Your article paragraphs go here...</p>
  <p>Each paragraph will be properly styled.</p>
</ArticleBody>
-->
<script>
  let {
    children,         // The content passed between opening/closing tags
  } = $props();
</script>

<article class="article-body">
  {@render children()}
</article>

<style lang="scss">
  @use '../styles' as *;

  /* Mobile-first: smaller text */
  .article-body {
    font-family: var(--font-sans);
    font-size: var(--font-size-lg);
    line-height: 1.8;
    color: var(--color-text);
  }

  /* Paragraph styling */
  .article-body :global(p) {
    margin-bottom: 1.5rem;
  }

  .article-body :global(p:last-child) {
    margin-bottom: 0;
  }

  /* Links within article body */
  .article-body :global(a) {
    color: var(--color-link);
    text-decoration: none;
    text-underline-offset: 0;
    border-bottom: 1px solid var(--color-link);
  }

  .article-body :global(a:hover) {
    color: var(--color-link-hover);
    border-bottom-color: var(--color-link-hover);
  }

  /* Subheadings within article */
  .article-body :global(h2) {
    font-family: var(--font-serif);
    font-size: 1.75rem;
    font-weight: 400;
    margin-top: var(--spacing-xl);
    margin-bottom: var(--spacing-sm);
    color: var(--color-dark);
  }

  .article-body :global(h3) {
    font-family: var(--font-serif);
    font-size: 1.375rem;
    font-weight: 400;
    margin-top: var(--spacing-lg);
    margin-bottom: var(--spacing-sm);
    color: var(--color-dark);
  }

  /* Block quotes - NYT style with left border */
  .article-body :global(blockquote) {
    border-left: 4px solid var(--color-medium-gray);
    margin: var(--spacing-lg) 0;
    padding: 0 var(--spacing-md);
    font-style: italic;
    font-size: var(--font-size-base);
    line-height: 1.8;
    color: var(--color-text);
  }

  .article-body :global(blockquote p) {
    margin-bottom: 0;
  }

  /* Lists */
  .article-body :global(ul),
  .article-body :global(ol) {
    margin-bottom: var(--spacing-md);
    padding-left: var(--spacing-md);
  }

  .article-body :global(li) {
    margin-bottom: var(--spacing-xs);
  }

  /* Strong/Bold text */
  .article-body :global(strong) {
    font-weight: 600;
  }

  /* Tablet and up: larger text */
  @include tablet {
    .article-body {
      font-size: var(--font-size-lg);
      line-height: 1.8;
    }

    .article-body :global(blockquote) {
      font-size: var(--font-size-base);
    }
  }
</style>
