# Gestor de Tráfego

Painel web interno para acompanhamento de campanhas de **Google Ads** e **Meta Ads**.

## O que é

Aplicação web executada localmente no computador do responsável
(`http://localhost:3000`), que reúne em uma única interface as métricas das contas
de anúncios administradas por ele. Não é distribuída, publicada ou oferecida como
serviço a terceiros.

## O que faz

- Consolida investimento, impressões, cliques, conversões, receita, CTR, CPC, CPA e ROAS.
- Filtra por conta de anúncios, plataforma e período (7, 30 ou 90 dias).
- Mostra cada conta de anúncios separadamente.
- Compara o desempenho entre Google Ads e Meta Ads.
- Atualiza os dados sob demanda, por meio de sincronização manual.

## Uso da Google Ads API

A integração é **somente leitura**:

- Autenticação OAuth 2.0 com o escopo `https://www.googleapis.com/auth/adwords`
  e `access_type=offline`.
- `customers:listAccessibleCustomers` para identificar as contas acessíveis.
- Consultas GAQL via `googleAds:searchStream`, uma vez por conta:
  - `customer.id`, `customer.descriptive_name`, `customer.currency_code`
  - `campaign.id`, `campaign.name`, `campaign.status`,
    `campaign.advertising_channel_type`, `campaign.start_date`
  - `campaign_budget.amount_micros`
  - `metrics.impressions`, `metrics.clicks`, `metrics.cost_micros`,
    `metrics.conversions`, `metrics.conversions_value`
  - segmentadas por `segments.date`, limitadas aos últimos 90 dias

A ferramenta **não** cria, altera, pausa ou remove campanhas, orçamentos, grupos
de anúncios, anúncios, palavras-chave ou públicos. Não realiza uploads e não
acessa dados de faturamento.

## Dados e segurança

- Credenciais e métricas ficam apenas no computador do responsável, em arquivos locais.
- Tokens são criptografados com AES-256-GCM; a chave é mantida em arquivo local separado.
- Nenhum dado é compartilhado com terceiros, revendido ou publicado.
- A ferramenta não possui cadastro de usuários e não é multiusuário.

## Escopo

Uso pessoal e interno, restrito às contas das quais o responsável é administrador
ou que lhe concederam acesso explícito via OAuth.

## Contato

Sérgio Alexandre Pereira — sergioalex32.pereira@gmail.com
