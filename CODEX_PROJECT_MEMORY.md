# CODEX Project Memory

Project root: `C:\Desenvolvimento\DelphiSGACodex`

## Operating Rules

- Read this file before source-code work in this repo.
- Work in `C:\Desenvolvimento\DelphiSGACodex` by default.
- Do not edit `C:\Desenvolvimento\DelphiSGA` unless the user explicitly
  approves that specific write. Treat it as read-only reference.
- Shared memory lives in `C:\Desenvolvimento\CodexMemoria` and is versioned
  at `https://github.com/brunosilvadelphionline-png/CodexMemoria`.
- Before implementation tasks that change source code, pull the shared memory
  repository first with
  `git -C C:\Desenvolvimento\CodexMemoria pull --ff-only origin main`, then
  read the relevant memory files before editing code.
- When any file under `C:\Desenvolvimento\CodexMemoria` is changed, commit
  and push that repository immediately so other developers stay synchronized.
- For source-code tasks, run `git status --short` first. If clean, use
  `master` and pull `origin master`; if dirty, do not switch, pull, overwrite,
  or revert without asking.
- For memory/configuration cleanup or non-code conversation tasks, do not pull
  the source-code repository.
- User-facing Portuguese text must use accents and natural spelling. Internal
  memory notes should stay ASCII when practical.
- Classify requests:
  - analysis: investigate and answer; do not edit code.
  - implementation: inspect, edit, and validate.
  - support/triage: draft responses, estimates, or next steps; no code edits
    unless explicitly requested.

## Subject Memories

Keep this main file small. Store durable process-specific notes in subject
files and read only the relevant file for the task.

- Production, diaria de producao, automacao, equipamento, CEQ, eventos de
  producao, `ProdutosProduzidos`: read `codex-memory/producao.md`.
- Fiscal, NF-e, NFSe, CT-e, CFOP, natureza, XML, SPED: read
  `codex-memory/fiscal.md`.
- Integrations, SgaWS, eSocial, portal bridge, API/service signatures: read
  `codex-memory/integracoes.md`.
- Financeiro, Contas a Pagar, cobranca bancaria, remessa/retorno: read
  `codex-memory/financeiro.md`.
- Contabilidade, Ativo Imobilizado, depreciacao: read
  `codex-memory/contabilidade.md`.

## Tooling

- Prefer `rg` / `rg --files` for searches.
- Many Delphi files are legacy ANSI/Windows-1252 with CRLF. If `apply_patch`
  fails on Delphi source, edit with PowerShell using
  `[System.Text.Encoding]::Default` and preserve CRLF.
- Use this whitespace check to avoid CRLF noise:
  `git -c core.whitespace=blank-at-eol,blank-at-eof,space-before-tab,cr-at-eol diff --check`
- `dcc32.exe` exists at
  `C:\Program Files (x86)\Embarcadero\Studio\23.0\bin\dcc32.exe`, but this
  install reports that command-line compiling is not supported.

## General Patterns

- New global helpers should live in the base unit for the subject area. Example:
  NF-e helpers in `SgaExp\SgaExpNf.pas`; only use `Sga\SgaArq.pas` for truly
  generic cross-area helpers.
- Global parameter variables live in `Sga\SgaParam.pas`.
- Parameter read pattern: `ReadPar(emp, fil, <id>, 0, Param...)`.
- `Sga\SgaParam.pas` caches company parameters in `ListaPar`; keep it sorted
  after loading so `ReadPar` lookups use `TStringList` binary search.
- Parameter save pattern:
  `PreparaChavePar(<id>, 0, emp, fil); FieldByName(...); Post;`.
- Boolean `PARCHAR` parameters commonly use `SimNao[BooleanParam]`.
- For database structure changes, update `SgaSql\SGA.SQL` and `ALTER.TXT`.
  `ALTER.TXT` uses InterBase syntax, `;` per command, and `#` alone as the
  separator. Do not add generator initialization commands.
- Do not change `SgaSql\Sga_Oracle.SQL` unless the user explicitly asks for
  Oracle script changes.
- For new Delphi labels, prefer descriptive component names instead of generic
  `LabelX` names.
