<!--
@license
Copyright (c) Audanika. All Rights Reserved.

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Add the dna_blog and dna_translate layers

## Motivation

- This layer is the umbrella of the audanika DNA: a repo adds it once and
  gets every topic layer. Its README promised the blog format and the
  translations, but neither `dna_blog` nor `dna_translate` was in the
  list of layers.
- The gg review step writes a blog post in every repo that has
  `doc/guides/blog-guide.md`. Without the layer no audanika repo had the
  guide, so no post was written and the pull requests carried no
  documentation of their change.
- `dna_translate` had been removed from the umbrella on 2026-10-06. The
  german counterparts of guides, README files and posts are wanted again,
  so the layer returns together with the blog layer it complements.

## Strategy

- Add both layers to `dna/_dna.json` right after `dna_index`, so the
  layers that write guides come before the ones that place skills and
  workflows.
- Declare them in `pubspec.yaml` and let the own DNA test instantiate
  what they bring, so the repo shows what a consumer will get.
- Lift the dependency constraints of all layers to their latest versions
  in the same ticket; `gg do push` does that on its own, so the ticket
  faces the new requirements once instead of every later ticket.
- Describe the repo in `index.jsonc`, which it did not have yet.

## Implementation 1: the layers

- `dna_blog` 0.3.0 brings `doc/guides/blog-guide.md`,
  `doc/templates/blog-template.md` and the `/blog` skill. Posts go to
  `doc/blog/<yyyy>/<yyyy>-<mm>-<dd>-<title>.md`, which is where this post
  lives.
- `dna_translate` 0.3.0 brings `doc/guides/translate-guide.md`,
  `doc/templates/blog-template-de.md` and the `/translate` skill.
- Both are orthogonal layers with no parents of their own; they only ask
  for `dnaCopyrightHolder`, which `dna/_vars.json` sets already.
- The layer table of the README lists both; the new `index.jsonc` names
  them under `interfaces.uses`.

## Implementation 2: the upgrade of the other layers

- `dna_clean_code` 0.3.0, `dna_gg` 1.1.0, `dna_guides` 0.2.0,
  `dna_index` 0.2.0, `dna_install` 0.2.0, `dna_readme` 0.3.1,
  `dna_vscode` 0.4.0 and `dna_github` 0.1.1 replace the versions of
  October 6.
- `dna_github` 0.1.1 marks `dnaGitQuickCheckPipelineName` as a variable
  every layer below must set. `dna/_vars.json` now sets it to
  `Quick Check`, the job name of the quick check workflow and the status
  check the GitHub ruleset requires. It is the same value the layers
  default to, so consumers see no change.
- The instantiation moved `guides/setup-github-guide.md` to
  `doc/guides/`, added `scripts/check-readme.js`, the prompt hooks under
  `.claude/hooks` and the `gg-review` skill, and refreshed the guides,
  templates and skills to their current wording.

## Dependency updates

- `dna_gg` 1.0.0 and 1.1.0 add the review skill, the prompt hooks and the
  index of the gg skills; `dna_readme` 0.3.x adds the README check script.
  Everything else is a wording update of guides and templates.

## Open Points

- The Usage section of the README still describes the layer as consumed
  straight from git, although it is published on pub.dev; it is adjusted
  in a later ticket.
- pub.dev holds 0.0.2 while `main` still declares 0.0.1 in
  `pubspec.yaml`: 0.0.2 was published without its commit. The next
  release is a minor increment and goes above both.
- Every audanika repo takes the new layers with its next DNA build; the
  private DNA has to lift its constraint on this package first.
