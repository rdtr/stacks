# Authoring guide

## Purpose

This book exists first for its author's own learning. Every page is written by
the author, in the author's own words, after reading the code. AI assistance is
used for navigating code, fact-checking, diagram drafts, and review, never for
writing pages the author has not understood and verified.

## Layout

- `content/<volume>/`: one directory per volume (`spark`, later `gluten`, ...)
- `content/<volume>/NN-chapter/_index.md`: a chapter; its sections are sibling files
- `content/techniques/`: cross-cutting articles comparing one technique across engines

Create a new page from the template:

```bash
hugo new content spark/05-expressions/_index.md
```

## Versions

The book follows new releases on a best-effort basis instead of freezing on one.

- `params.targets` in `hugo.yaml` lists the versions the book currently tracks.
- Each page records the versions it was checked against:

  ```yaml
  verified:
    spark: v4.2.0
  ```

  Pages about several engines list each one. A page whose `verified` version
  differs from `params.targets` shows an "out of date" banner.

## Linking to source code

Use the `src` shortcode instead of hand-written GitHub URLs:

```
{{< src repo="spark" path="sql/catalyst/src/main/scala/org/apache/spark/sql/catalyst/expressions/Expression.scala" anchor="abstract class Expression extends" />}}
{{< src repo="spark" path="..." anchor="..." span="3" >}}`Expression.eval`{{< /src >}}
```

- The link points at the page's `verified` version of `repo`.
- `anchor` is text on the target line. The line number is found at build time,
  so links follow code that moves between versions. Pick text that matches only
  one line; a missing or ambiguous anchor is a build warning locally and fails CI.
- `span` highlights extra lines after the anchor line.
- Repositories are registered under `params.repos` in `hugo.yaml`.

## Chapter template

Each chapter uses the same sections (see `archetypes/default.md`):

1. Questions this chapter answers
2. Overview
3. Code walkthrough
4. Experiments
5. Comparison with other engines
6. Version history
7. References
