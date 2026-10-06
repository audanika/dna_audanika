# dna_audanika

The DNA of every audanika repo: one dependency that pulls in the whole
set of topic layers.

Add this one layer and a repo gets the README structure, the guides, the
translations, the index, the blog format, the install guides, the VS Code
settings, the clean code and test conventions, and the gg workflow.

## Layers

| Layer | What it brings |
| --- | --- |
| [dna_readme](https://github.com/ggdna/dna_readme) | README structure and templates |
| [dna_guides](https://github.com/ggdna/dna_guides) | developer and AI guides |
| [dna_translate](https://github.com/ggdna/dna_translate) | multi-language docs, de and en in sync |
| [dna_index](https://github.com/ggdna/dna_index) | index and navigation files |
| [dna_blog](https://github.com/ggdna/dna_blog) | blog format, templates, layout |
| [dna_install](https://github.com/ggdna/dna_install) | install guides: editor, node, Azure, tooling |
| [dna_vscode](https://github.com/ggdna/dna_vscode) | shared editor settings and extensions |
| [dna_clean_code](https://github.com/ggdna/dna_clean_code) | how code is written and tested, incl. the Dart specifics |
| [dna_gg](https://github.com/ggdna/dna_gg) | the gg workflow, and the scripts it calls |

Beyond composing the layers above it carries one file of its own,
`dna/LICENSE`: audanika repos all share the same
license, so the layer ships it instead of every repo keeping
its own copy. The engine refuses to finish without a LICENSE.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file,
  set to `Dr. Gabriel Gatzsche. All Rights Reserved.` here, so a header
  reads `Copyright (c) Dr. Gabriel Gatzsche. All Rights Reserved.`

## Usage

Declare this layer as a dev-dependency of your package and initialize
once:

```bash
gg dna add dna_audanika
gg dna init
```

That writes the dependency into `pubspec.yaml` and lists the layer in
`dna/_dna.json`. The placed test instantiates and verifies the DNA on
every test run.

To adapt something for a single repo, override it there: a same-path file
replaces the inherited one, `X.overrides.json` merges field-wise, and
`X.overrides.md` replaces only the tagged sections of a guide.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
