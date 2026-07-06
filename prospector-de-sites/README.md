# Prospector de Sites

Prospecção semi-automática de clientes com sites ruins: acha, redesenha, publica e oferta.

## O ciclo

1. `/setup` — roda uma vez: assinatura, nichos padrão, dados do cPanel da HostGator (com teste de publicação).
2. `/prospectar [nicho] [cidade]` — busca no Google Maps negócios nota ≥ 4.7 com site fraco e gera `leads.md` com e-mail, motivo e ranking (padrão: 10 leads).
3. `/redesenhar` — recria as páginas dos 5+ melhores leads com estética premium, mantendo o conteúdo, logo e paleta reais do cliente.
4. `/editor [cliente]` — gera versão editável no navegador (textos e imagens) com exportação da página final.
5. `/publicar [cliente|todos]` — sobe na HostGator em `dominio.com/clientes/[slug]/` e verifica a URL.
6. `/proposta [cliente|todos]` — escreve o e-mail (rapport, sem preço) e cria o rascunho no Gmail.

## Requisitos

- Extensão Claude in Chrome conectada (prospecção no Maps e fallback de deploy)
- Conector do Gmail (rascunhos de proposta)
- Pasta conectada no Cowork (armazena config, leads e sites)
- Hospedagem HostGator com acesso ao cPanel

## Onde ficam os dados

Tudo na pasta conectada: `prospector-config.json` (preferências e credenciais — a senha do cPanel fica em texto no seu computador), `leads.md` (pipeline) e `sites/[slug]/` (páginas criadas).
