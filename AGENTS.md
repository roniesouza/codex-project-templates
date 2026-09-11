## Objetivo

Descrição simplificada e pragmática do projeto.

Prioridades, nesta ordem:

1. Simplicidade
2. Segurança
3. Performance

Sempre buscar a solução mais simples que atenda corretamente ao requisito. Evitar abstrações, dependências, configurações e funcionalidades desnecessárias.

## Regras gerais

* Usar Python.
* Usar `uv` para gerenciar projeto e dependências.
* Usar `Ruff` como linter.
* Seguir PEP 8.
* Usar `logging` para logs operacionais; evitar `print` para esse fim.
* Manter o código simples, legível e objetivo.
* Priorizar a biblioteca padrão do Python quando adequada.
* Adicionar dependências somente quando trouxerem benefício claro.
* Não criar funcionalidades não solicitadas.
* Não alterar comportamento existente sem necessidade.
* Não expor senhas, tokens, credenciais ou outros segredos.
* Nunca versionar `.env` ou arquivos contendo segredos.
* Não usar `shell=True` quando comandos puderem ser executados diretamente com `subprocess`.
* Falhas relevantes devem produzir erro de forma explícita e adequada ao contexto.

## Subagentes

Usar subagentes somente quando trouxerem ganho claro de qualidade, segurança ou paralelismo.

* Para tarefas simples e bem delimitadas, o agente principal deve executar diretamente.
* Usar `explorer` quando for necessário entender fluxo, dependências ou impacto antes de alterar.
* Usar `maintainer` para implementações e manutenções bem delimitadas quando a delegação for útil.
* Usar `verifier` para validações relevantes após alterações.
* Usar `reviewer` para mudanças relevantes ou quando houver risco de regressão.
* Usar `documentation` para criação ou atualização substancial de documentação.
* Usar `git_operator` somente quando operações Git forem explicitamente solicitadas.
* Ao delegar, atribuir a cada subagente uma tarefa clara e não sobreposta.
* Não delegar quando o custo de coordenação for maior que o benefício esperado.
* Não criar subagentes desnecessariamente para tarefas triviais.

## Configuração

Quando houver configuração por ambiente, preferir variáveis de ambiente.

Quando `.env` for utilizado:

* manter `.env` fora do Git;
* fornecer `.env.example` sem valores sensíveis;
* documentar somente as variáveis necessárias.

Validar configurações obrigatórias antes de iniciar operações dependentes delas.

Evitar configurações desnecessárias ou valores configuráveis sem necessidade concreta.

## Interface

Quando o projeto possuir CLI:

* manter a interface pequena e previsível;
* evitar comandos e flags sem necessidade real;
* preservar compatibilidade quando possível;
* fornecer mensagens de erro claras;
* evitar adicionar dependências quando `argparse` for suficiente.

## Logs

Usar o módulo padrão:

```python
logging
```

Registrar informações úteis para acompanhamento e diagnóstico, de forma proporcional ao projeto.

Nunca registrar:

* senhas;
* tokens;
* credenciais;
* variáveis contendo segredos;
* comandos completos contendo informações sensíveis.

Evitar logs excessivos ou que apenas repitam informações sem valor operacional.

## Estrutura do código

Manter poucos arquivos e responsabilidades claras.

Evitar fragmentar prematuramente o projeto em muitos módulos.

Criar módulos adicionais quando isso melhorar claramente:

* coesão;
* legibilidade;
* manutenção;
* reutilização.

Não criar classes quando funções simples forem suficientes.

Não aplicar padrões como repository, service, factory ou dependency injection sem necessidade concreta.

Não criar camadas adicionais apenas por convenção ou antecipação de necessidades futuras.

## Performance

Otimizar primeiro os pontos que realmente afetam o tempo, memória ou recursos utilizados pelo projeto.

Não trocar simplicidade por micro-otimizações sem ganho mensurável ou necessidade concreta.

Evitar processamento, I/O e alocações desnecessárias quando identificados como relevantes.

Sempre que houver duas soluções equivalentes, preferir a mais simples.

## Segurança

Não imprimir ou registrar segredos.

Não versionar:

* `.env`;
* credenciais;
* chaves;
* tokens;
* arquivos contendo dados sensíveis.

Validar entradas externas quando houver risco relevante.

Evitar executar comandos construídos a partir de entrada não confiável.

Aplicar o princípio do menor privilégio quando houver acesso a recursos externos.

Não reduzir segurança apenas para simplificar a implementação.

## Erros

Falhar cedo quando uma condição obrigatória para a operação não estiver satisfeita.

Exemplos:

* configuração obrigatória ausente;
* entrada inválida;
* recurso necessário indisponível;
* impossibilidade de criar ou acessar arquivo ou diretório necessário.

Preservar contexto suficiente para diagnóstico de falhas sem expor informações sensíveis.

Não ocultar exceções sem motivo.

Não capturar exceções genéricas quando uma exceção mais específica puder ser tratada adequadamente.

Não transformar erros relevantes em sucesso silencioso.

## Qualidade

O código deve:

* seguir PEP 8;
* passar pelo Ruff;
* possuir nomes claros;
* manter funções com responsabilidades compreensíveis;
* evitar duplicação relevante;
* utilizar tipagem quando melhorar clareza, segurança ou manutenção;
* evitar complexidade acidental;
* preservar consistência com o restante do projeto.

Quando aplicável:

* usar `pathlib` para caminhos;
* usar `subprocess` com argumentos em lista;
* usar `time.monotonic()` para medir intervalos de tempo;
* preferir `argparse` para CLIs simples antes de adicionar dependências.

Evitar comentários que apenas repetem o código.

Comentar decisões importantes, especialmente quando envolverem:

* segurança;
* compatibilidade;
* limitações técnicas;
* comportamento não óbvio.

## Testes e validação

As validações devem ser proporcionais ao risco e ao escopo da alteração.

* Executar primeiro as verificações mais específicas e de menor custo.
* Ampliar a validação quando o risco ou a alteração justificar.
* Não criar testes artificiais apenas para aumentar cobertura.
* Preservar testes existentes e corrigir regressões causadas pela alteração.
* Adicionar ou atualizar testes quando forem relevantes para garantir comportamento importante.
* Não considerar uma alteração concluída quando verificações obrigatórias do projeto estiverem falhando por causa dela.
* Diferenciar falhas introduzidas pela alteração de falhas preexistentes.

## Ruff

Usar Ruff como linter oficial do projeto.

Adicionar como dependência de desenvolvimento usando `uv`:

```bash
uv add --dev ruff
```

Executar antes de considerar uma alteração concluída:

```bash
uv run ruff check .
```

Quando aplicável, correções automáticas podem ser executadas com:

```bash
uv run ruff check . --fix
```

Configurar o Ruff no `pyproject.toml`.

Manter a configuração simples e próxima dos padrões do Ruff.

Adicionar, alterar ou ignorar regras somente quando houver necessidade concreta.

Não desabilitar regras globalmente apenas para evitar corrigir código inadequado.

## Code review

Revisar a unidade de trabalho completa antes da integração:

```text
implementar → validar → commit(s) → review → corrigir → validar novamente → push/merge
```

* Com Pull Request, revisar antes do merge.
* Com envio direto à branch principal, revisar antes do push final.
* Não exigir review para cada alteração intermediária; repetir quando houver mudanças relevantes.
* Revisar código, diff e comportamento afetado.
* Priorizar requisitos, correção, regressões, segurança, tratamento de erros, performance e simplicidade.
* Avaliar a necessidade de testes conforme o risco, o comportamento alterado e as práticas existentes no projeto.
* Executar as verificações obrigatórias definidas pelo projeto.
* Apresentar problemas por severidade, com arquivo e linha quando possível.
* Não alterar código durante o review sem solicitação explícita.
* Evitar comentários puramente estéticos quando não houver impacto relevante.
* Se não houver problemas relevantes, informar explicitamente que não foram encontrados achados bloqueantes.

Escolher sempre a solução mais simples que atenda aos requisitos.

## Commits

Todos os commits devem seguir Conventional Commits:

```text
<tipo>(<escopo opcional>): <descrição>
```

Tipos permitidos:

```text
feat
fix
docs
refactor
test
chore
```

Manter o tipo em inglês.

Escrever a descrição curta, objetiva e em português.

Exemplos:

```text
feat: adiciona validação de configuração

fix: corrige tratamento de entrada inválida

docs: atualiza instruções de uso

refactor: simplifica fluxo de processamento

test: adiciona cobertura para cenário de erro

chore: atualiza configuração de desenvolvimento
```

Antes de criar qualquer commit:

* verificar o diff;
* confirmar que somente arquivos relacionados ao escopo estão preparados;
* não incluir segredos, credenciais ou artefatos locais;
* respeitar convenções adicionais definidas pelo projeto.

Quando o projeto utilizar card, issue ou demanda associada ao trabalho, confirmar o identificador antes de incluí-lo.

Quando houver identificador, incluir preferencialmente no rodapé:

```text
Refs: <CARD-ID>
```

Exemplo:

```text
feat: adiciona validação de configuração

Refs: ABC-123
```

Nunca inventar identificadores.

Não exigir referência a card ou demanda quando o projeto ou a tarefa não utilizar esse processo.

## Critério de decisão

Ao implementar, revisar ou modificar qualquer parte do projeto, considerar nesta ordem:

1. Existe uma solução mais simples?
2. É segura?
3. Preserva o comportamento e os contratos que não fazem parte da mudança?
4. É eficiente o suficiente para o requisito?
5. É realmente necessário adicionar essa complexidade?

Se duas soluções atenderem ao requisito, preferir a que tiver menos código, menos dependências, menos estados e menor complexidade operacional.
