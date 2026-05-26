# Codex Project Instructions

This repository is the preferred working project:

`C:\Desenvolvimento\DelphiSGACodex`

Do not edit files under `C:\Desenvolvimento\DelphiSGA` unless the user gives
explicit approval for that specific action. If a task references a file in
`C:\Desenvolvimento\DelphiSGA`, treat it as reference/read-only by default,
explain why editing there would be needed, and ask before writing. Prefer the
equivalent file under `C:\Desenvolvimento\DelphiSGACodex` for code changes.

At the start of future sessions in this repo, read `CODEX_PROJECT_MEMORY.md`
before making changes. Use it as the local project memory.

For source-code-related project tasks only, update `master` before working.
This applies when the user asks what the project/code does, asks for code
analysis/debugging, or requests a project change. For conversations, text
drafts, estimates, memory/configuration updates, or anything not tied to code
understanding/changes, do not run `git pull`.

1. Run `git status --short`.
2. If the working tree is clean, switch to `master` if needed and run
   `git pull origin master`.
3. If there are local changes, do not overwrite or revert them. Ask the user
   before switching branches or pulling in a way that could affect those
   changes.

When you learn a durable project pattern, update `CODEX_PROJECT_MEMORY.md`
with a short note. Keep notes practical and concise:

- where important features live;
- how configuration/parameters are stored;
- build or verification commands that work or fail;
- encoding/tooling gotchas;
- decisions from implemented tasks.

Keep notes in ASCII to avoid encoding churn in this legacy Delphi repository.
Do not add speculative notes; record only facts observed in the code or during
work in this project.

## Intent routing

Classify the user's request before acting and use the matching work mode:

- Question / analysis mode: for requests like "me diga a regra", "como
  funciona", "qual chamado criou", "onde fica", or "resuma". Investigate only
  what is needed, do not edit code, and answer with the rule, code/history
  references, or a client-ready explanation.
- Implementation mode: for requests like "ajustar", "corrigir", "criar
  parametro", "implementar", or "alterar". Follow the startup git checks,
  inspect impact, edit files, and verify what is feasible before finalizing.
- Support / triage mode: for requests like "como responder", "estimar",
  "avaliar demanda", or "montar texto". Provide a practical response,
  estimate, or next-step guidance without changing code unless explicitly
  requested.

If the intent is ambiguous, prefer question / analysis mode and keep the
response concise. Switch to implementation mode only when the user clearly asks
for a code or configuration change.

## Effort reporting

For every source-code-related task, including analysis, behavior/history
questions, debugging, review, and implementation, include an estimated effort
summary in the final response.

Do not claim exact token usage, exact plan consumption, or exact quota usage.
Those values are not visible from this environment. Report only observable or
reasonable estimates that can help the user build an Excel history for plan
selection.

Use this compact format when possible:

`Metrica da tarefa: tempo aproximado X min; tipo <analise|implementacao|debug|review|triagem>; intensidade <baixa|media|alta>; ferramentas N comandos/buscas; arquivos lidos N; arquivos alterados N; validacao <sim/nao>; consumo real do plano: nao mensuravel pelo Codex.`

Suggested Excel columns for the user:

- Data
- Tipo da tarefa
- Resumo
- Tempo aproximado (min)
- Intensidade
- Comandos/buscas
- Arquivos lidos
- Arquivos alterados
- Validacao executada
- Resultado
- Consumo real observado pelo usuario
- Observacoes
