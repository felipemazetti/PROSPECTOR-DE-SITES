---
name: prospeccao-web
description: Variante para Codex da prospecção de clientes — encontra negócios locais bem avaliados com sites ruins usando pesquisa assistida na web (busca + fontes públicas + verificação cruzada), sem depender de automação do Google Maps. Acione quando o usuário pedir "prospectar", "buscar clientes", "achar leads" ou invocar $prospectar no Codex.
---

# Prospecção por pesquisa assistida na web (Codex)

Mesmo objetivo da skill `prospeccao-maps` do plugin: encontrar o cliente ouro — negócio que JÁ fatura bem (nota alta, muitas avaliações) mas perde clientes por causa de um site fraco. O que muda é o MÉTODO: aqui não há automação do Google Maps; a descoberta é por **pesquisa assistida** com as ferramentas de busca/navegação disponíveis no Codex.

## Método (pesquisa assistida, não scraping)

1. **Descoberta**: busque na web `[nicho] em [cidade]` e variações (`melhores [nicho] [cidade]`, `[nicho] [bairro]`). Compile candidatos dos resultados locais, diretórios públicos e listas do próprio Google. Monte uma lista de 20-30 nomes antes de qualificar.
2. **Verificação da avaliação** (por candidato): busque `[nome do negócio] [cidade] avaliações` — a nota e o nº de avaliações do Google aparecem no snippet do perfil público do negócio. Registre nota, nº de avaliações e a fonte. **Se não conseguir verificar nota/avaliações em fonte pública, o lead NÃO qualifica** — anote como "não verificado" e siga.
3. **Filtros (idênticos aos do plugin)**:
   - **Potencial financeiro**: nota ≥ 4.7 E avaliações ≥ 40. Reprovou → próximo.
   - **TEM site próprio**: busque `[nome] [cidade] site` e abra o resultado. Sem site, site fora do ar, ou "site" que é diretório de terceiros/linktree/só Instagram → descartar (registrar motivo) e seguir.
   - **Site ruim**: abra o site e avalie pelos critérios da skill `prospeccao-maps` (layout datado, sem CTA, não responsivo, domínio gratuito, conteúdo desorganizado, sem prova social). 2+ problemas = candidato. O motivo anotado deve ser objetivo e verificável — será citado na proposta.
4. **E-mail é obrigatório**: procure no site (rodapé, página de contato, `mailto:`), depois busca por `[nome] email contato`. Sem e-mail público → descartar (registrando o contato que existir) e continuar até a meta.
5. **WhatsApp**: capture do site (`wa.me/`, `api.whatsapp.com`) ou telefone celular público (9º dígito = celular no Brasil). Formato `55DDDnúmero`.
6. **Verificação cruzada**: antes de qualificar, confirme que o negócio está ativo (horários/avaliações recentes em fonte pública) e que os dados batem entre pelo menos 2 fontes (ex.: site + perfil do Google). Dado divergente = anotar a dúvida, não inventar.
7. Pare ao atingir a meta do config (padrão 10 qualificados) ou após avaliar 25 estabelecimentos. Pule quem já está em `leads.md`.

## Conformidade (inegociável)

- O navegador/busca é ferramenta de PESQUISA, não de scraping em massa: um negócio por vez, volume humano.
- Respeite captchas, rate limits e paywalls — se aparecerem, PARE essa fonte e use outra (ou avise o usuário). Nunca contorne controle de acesso.
- Só dados públicos de negócios (nada de dado pessoal sem justificativa — o e-mail comercial público é o lastro, ver seção LGPD da skill `proposta-email`).
- **NUNCA invente ou "estime" nota, avaliações, e-mail ou telefone.** Campo não verificado fica vazio com a anotação "não verificado". Um lead com dado inventado destrói a proposta (o elogio da abordagem cita a nota real).

## Saída (adaptada ao Codex — sem conector do Google Drive)

1. **CSV local**: `leads-[nicho]-[cidade].csv` na pasta de trabalho, colunas: `#, Nome, Nota, Avaliações, E-mail, Telefone, WhatsApp, Site atual, Motivo, Situação (Qualificado/Descartado), Fonte da verificação, Status, URL nova`. Qualificados E descartados, ranqueados por potencial (nota alta + site pior primeiro).
2. **`leads.md`** e **dashboard** (banco + snapshot) exatamente como a skill `dashboard-leads` manda — leads novos com `status: novo`, descartados com `status: descartado`. Nunca duplicar cliente já avaliado.
3. Tabela-resumo no chat com os qualificados e os 3 melhores alvos, e o próximo passo: `$redesenhar`.
