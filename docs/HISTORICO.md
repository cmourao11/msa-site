# Histórico — MMS Site

> Itens concluídos, mergeados e deployados. Lições de ouro preservadas.

## 2026-06-14

### Camada de animação/UX profissional (PR #1, mergeado + deployado)
Reveal em cascata via `IntersectionObserver`, barra de progresso de leitura, navbar com sombra ao
rolar, parallax leve no hero, press nos CTAs, hover nos cards — tudo respeitando
`prefers-reduced-motion`. Também corrigiu a mensagem do WhatsApp e a copy de posicionamento
(assessoria hospitalar → administração de clínicas e hospitais).

### Lições de ouro (ambiente / bundle)
- O conteúdo dos HTMLs vive em 3 blocos `<script type="__bundler/...">`:
  - `__bundler/manifest`: JSON `{ assetId: { mime, compressed, data(base64) } }` — imagens e fontes.
  - `__bundler/ext_resources` e `__bundler/template`: HTML+CSS+JS como string JSON escapada.
- **Trocar imagem** = substituir `data` (base64) do `assetId` no manifest dos 2 arquivos. Validar
  com sha256 (bytes embutidos == arquivo original). `<img src="ASSET_ID">` é resolvido em runtime.
- **Editar template** = parse JSON → alterar string → `ConvertTo-Json -Compress` (escapa `<` e `/`,
  então `</script>` interno não fecha o `<script>` real).
- Regex frágil falha silenciosamente em blocos grandes — preferir IndexOf + slice por âncoras exatas.
- Validar sem browser: `JSON.parse` dos blocos + `new vm.Script(...)` no componente. Playwright não
  instalado; não instalar só para validar.
