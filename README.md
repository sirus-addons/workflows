Общий workflow выпуска релизов для аддонов sirus-addons.

Каждый аддон подключает его файлом `.github/workflows/action.yml`:

```yaml
name: Addon release
'on':
  push:
    branches:
      - master
    paths-ignore:
      - '.github/**'
      - '.screenshots/**'
      - 'README.md'
  workflow_dispatch:
permissions:
  contents: write
jobs:
  release:
    uses: sirus-addons/workflows/.github/workflows/addon-release.yml@master
```

Релиз создаётся при пуше в `master`, кроме пушей, которые меняют только
`.github/`, `.screenshots/` или `README.md`. Пропущенный релиз можно
запустить вручную: Actions → Addon release → Run workflow.

Релиз: тег `<sha7>-<ГГГГММДДЧЧММ>` (UTC), название
`<repo> - <ГГГГ-ММ-ДД ЧЧ:ММ>`, архив `<repo>.zip` без служебных файлов
(`.git*`, `.github/`, `.screenshots/`, `.vscode/`, `.idea/`, `README.md`,
`addon-meta.yml`).
