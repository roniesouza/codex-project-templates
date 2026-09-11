# Codex Python Template

Arquivos-base reutilizáveis para projetos Python que usam Codex.

Este repositório não cria nem inicializa projetos. Ele fornece instruções e
configurações que podem ser copiadas ou usadas como ponto de partida em outro
repositório.

Inclui:

- `AGENTS.md` com regras gerais para projetos Python;
- `.codex/config.toml` com a configuração padrão do Codex;
- subagentes especializados em `.codex/agents/`.

## Estrutura

```text
.
├── .codex/
│   ├── agents/
│   │   ├── documentation.toml
│   │   ├── explorer.toml
│   │   ├── git_operator.toml
│   │   ├── maintainer.toml
│   │   ├── reviewer.toml
│   │   └── verifier.toml
│   └── config.toml
└── AGENTS.md
```

## Uso

Use este repositório como template no GitHub ou copie `AGENTS.md` e `.codex/`
para a raiz de um projeto Python.

Depois, ajuste o `AGENTS.md` com o objetivo e as regras específicas do projeto.

A configuração deve permanecer simples e ser expandida somente quando houver necessidade real.

## Referências oficiais

A estrutura e a configuração do Codex utilizadas neste template foram baseadas na documentação oficial da OpenAI. As convenções de desenvolvimento Python representam decisões deste template.

- [Codex IDE extension](https://developers.openai.com/codex/ide)
- [Config basics](https://developers.openai.com/codex/config-basic)
- [Custom instructions with AGENTS.md](https://developers.openai.com/codex/guides/agents-md)
- [Subagents](https://developers.openai.com/codex/subagents)

Este repositório é um template pessoal e não é um projeto oficial da OpenAI.
