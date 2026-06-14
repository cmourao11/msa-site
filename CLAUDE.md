# MMS — Site institucional

Site estático (HTML único auto-contido, deploy na Vercel). Responder em PT-BR.

## Stack / estrutura
- `index.html` e `MMS-standalone.html`: **mesmo bundle**, 2 cópias. Toda alteração precisa ser
  aplicada nos **dois** arquivos.
- O conteúdo real fica dentro de `<script type="__bundler/template">` como **uma string JSON**
  (HTML+CSS+JS escapados). Para editar: extrair o JSON, alterar a string, `JSON.stringify` de volta.
  - Regras de ouro ao editar o template:
    - `</script>` dentro da string DEVE ficar escapado no arquivo final (`ConvertTo-Json` do
      PowerShell já escapa `<` e `/`) — senão fecha o `<script>` real e quebra a página.
    - Componente UI = `class Component extends DCLogic { renderVals() {...} componentDidMount() {...} }`.
    - Animações respeitam `prefers-reduced-motion`.
- WhatsApp da Mirian: `5563992253493`.

## Validação (gate, sem browser)
- JSON decodifica: `JSON.parse` do bloco template nos 2 arquivos.
- Sintaxe do componente: compilar com `new vm.Script(...)` no Node.
- Conferir que componente antigo saiu e o novo entrou (busca por marcadores).
- Playwright NÃO instalado; não instalar só para validar.

## Git
- Branch própria → commit em PT-BR → push → PR. **Não mergear sem autorização** (commit em branch
  própria não precisa de autorização).

## Última alteração
- **Camada de animação/UX profissional** nos 2 HTMLs (reveal em cascata via IntersectionObserver,
  barra de progresso de leitura, navbar com sombra ao rolar, parallax leve no hero, press nos CTAs,
  hover nos cards) + correção da mensagem do WhatsApp e da copy de posicionamento
  (assessoria hospitalar → administração de clínicas e hospitais). Tudo com `prefers-reduced-motion`.

## Pendências abertas
- (nenhuma)
