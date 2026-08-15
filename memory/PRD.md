# PRD — Site Consulpam + Painel Admin

## Original Problem Statement
Clone de repositório GitHub (FastAPI + React + MongoDB). Preservar painel admin `/donaspainel` + backend; substituir site público pelo site clonado da Consulpam. Concurso público — inicialmente Guarda Civil Municipal de Sobral/CE, migrado para **Prefeitura Municipal de Forquilha/CE** — Edital 001/2026. Integrar formulários públicos ao backend (cadastros, tracking, PIX, Telegram).

## Idioma do Usuário
Português (pt-BR)

## Arquitetura
- **Backend**: FastAPI + MongoDB (`/api/*`).
- **Frontend público**: HTML estáticos em `/app/frontend/public/*.html`, roteados via middleware do `craco.config.js`.
- **Painel Admin**: React estático buildado em `/app/frontend/public/donaspainel/` — preservado do repo original.
- **Integrações**: Telegram Bot API (notificações), PIX EMV (geração de código).

## Páginas Públicas
- `/` — index.html (home — página institucional da Fundação CETREDE com o edital do concurso de Forquilha e botão "Fazer Inscrição")
- `/inscricao` — inscricao.html (formulário)
- `/confirmar-dados` — confirmar-dados.html (revisão)
- `/comprovante` — comprovante.html (recibo)
- `/pagamento` — pagamento.html (PIX + QR)

## Credenciais
- Admin `/donaspainel`: `donas` / `Seinao10@@`

## Implementado
- **[15/08/2026]** **Rebranding Forquilha/CE**:
  - Nova home `/` = página da Fundação CETREDE (arquivo enviado pelo usuário) com edital "Concurso Público da Prefeitura Municipal de Forquilha (CE)".
  - Botão "Fazer Inscrição" (azul `#194360`) injetado logo após o parágrafo do EDITAL Nº 001/2026, aponta para `/inscricao.html`.
  - Todos os links externos da CETREDE (menu, footer, PDFs externos, scripts, iframes) foram removidos/neutralizados para deploy standalone.
  - Link do EDITAL redirecionado para PDF local `/docs/29062026-edital-001-2026.pdf`.
  - Todas as referências "SOBRAL/Sobral" trocadas por "FORQUILHA/Forquilha" em: `inscricao.html`, `comprovante.html`, `confirmacao.html`, `pagamento.html`, `donainel/index.html`, `donainel/static/js/main.fda9cfa5.js` (título do painel admin: "Painel Guarda Civil Forquilha-CE").
- **[19/07/2026]** Correção de responsividade mobile: CSS `<style id="mobile-fix">` refinado nos 5 HTMLs.
- Rebranding Guarda Civil (dashboard).
- Modal home com logo oficial.
- Integração completa `POST /api/inscricoes/submit`, tracking PIX (generated/copied/downloaded), Telegram notifications.
- PIX BR Code gerado via `pix_generator.py`.
- Botão "voltar" na pág. pagamento; cabeçalho oficial em todas as pág.

## Backlog / Próximos Passos (P2)
- Fluxo end-to-end de teste real com submissão de inscrição + geração PIX + notificação Telegram.
- Substituir logo/cabeçalho das páginas internas (`inscricao.html`, `comprovante.html`, etc.) — ainda apresentam identidade "Instituto Consulpam"; considerar alinhar visualmente com a nova home CETREDE/Forquilha.
- Melhorar UX do menu (agora scrollável horizontalmente no mobile).
- Testar em tablet (768px) — pode precisar breakpoint intermediário.
