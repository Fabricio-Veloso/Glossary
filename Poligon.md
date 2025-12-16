# Glossário de Polygon

## Sumário:

1. Tópicos gerais.
2. Transição Web2 → Web3.
3. 📚 Como estudar isso de forma eficaz (método, não links).
4. 📚 Documentação essencial — Como usar sem se perder.
---
# Tópicos gerais:
## 🌍 1) Tópicos gerais: O que é uma sidechain?
- É uma blockchain separada, com validadores próprios, mas que:
  - se conecta a uma blockchain maior (ex.: Ethereum)
  - permite mover ativos entre elas (via bridges)
  - geralmente tem taxas menores e maior velocidade
  - tem segurança independente (menos robusta que Ethereum)
- Exemplo: **Polygon PoS**
- **Analogia:**  
  - Ethereum = rodovia federal  
  - Sidechain = estrada estadual conectada à rodovia  

---

## 🧱 2) Tópicos gerais: O que são appchains?
- Blockchain criada exclusivamente para um app ou grupo de apps
- Características:
  - regras próprias  
  - moeda própria  
  - recursos não divididos com outras aplicações  
- Plataformas: Polkadot, Cosmos, Polygon
- **Analogia:**  
  - Criar seu próprio condomínio fechado, em vez de morar num prédio compartilhado

---

## 🧩 3) Tópicos gerais: O que são SDKs neste contexto?
- SDK = Software Development Kit
- No mundo blockchain:
  - ferramentas, templates e contratos-base para criar blockchains ou smart contracts
  - funciona como “um kit para montar sua própria cadeia compatível com Ethereum”
- Exemplo: **Polygon CDK** para criar appchains EVM-compatíveis

---

## 🔄 4) Tópicos gerais: O que é compatibilidade EVM?
- EVM = Ethereum Virtual Machine
- Uma rede compatível com EVM permite:
  - escrever em Solidity/Vyper
  - fazer deploy da mesma forma que no Ethereum
- Exemplos: Polygon PoS, Polygon zkEVM
- **Analogia:**  
  - Como escrever um app em JavaScript e rodar no Chrome, Firefox e Edge sem mudar nada

---

## 🧑‍💻 5) Tópicos gerais: Solidity e Vyper são linguagens completas?
- Sim, mas com restrições:
  - ambiente totalmente determinístico  
  - não acessam rede, arquivos ou SO  
  - usadas exclusivamente para smart contracts  
- Estilos:
  - Solidity = C/JS  
  - Vyper = Python mais restrito  

---

## 🏗️ 6) Tópicos gerais: Diferença entre infra e infra on-chain
### Infra on-chain:
- contratos
- tokens
- governança
- regras imutáveis  

### Infra off-chain:
- front-end
- servidores
- indexadores
- validação de dados
- bots  

**Por quê off-chain existe?**  
Porque blockchain é lenta, cara e limitada em memória.

---

## 🔌 7) Tópicos gerais: O que são nodes / RPCs?
- **Node:**  
  - computador rodando o software da blockchain  
  - mantém cópia da rede e valida transações  

- **RPC:**  
  - endpoint HTTP para seu app falar com o node  
  - fornecido por Infura, Alchemy, QuickNode  
  - evita rodar seu próprio node (caro)

---

## 🔁 8) Tópicos gerais: O que são relayers e bridges?
- **Bridge:** conexão entre blockchains (ex.: Ethereum ⇄ Polygon)  
  - bloqueia token na A  
  - cria representação na B  
  - rastreia movimentações  

- **Relayer:**  
  - processo que carrega provas entre as chains  
  - segurança do sistema depende deles  
  - ponto crítico do ecossistema

### Bridge (Cross-chain Bridge)
Sistema que permite mover valor entre duas blockchains independentes.
Funciona travando tokens na chain de origem e criando (mintando) tokens representativos na chain de destino.

A segurança de uma bridge depende:
- dos contratos inteligentes envolvidos
- do modelo de validação (multisig, validadores, provas)
- do código da própria bridge

Bridges conectam **soberanias diferentes**.

---

### Lock & Mint
Modelo clássico de bridge:
- Lock: tokens originais são enviados para um contrato na chain de origem
- Mint: tokens equivalentes são criados na chain de destino

Enquanto os tokens estiverem travados, o usuário não pode utilizá-los na chain original.

---

### Burn & Unlock
Fluxo inverso do bridge:
- Burn: tokens representativos são destruídos na chain de destino
- Unlock: tokens originais são liberados do contrato na chain de origem

Garante que não exista double spend entre as chains.

---

### Relayer
Entidade que transporta mensagens ou provas entre blockchains.
Relayers:
- não criam verdade
- apenas transmitem dados
- podem ser não confiáveis, pois as mensagens são verificadas on-chain

---

### Fragilidade das Bridges
Bridges são historicamente o ponto mais vulnerável do ecossistema Web3.
Riscos comuns:
- bugs em contratos
- validação fraca de provas
- comprometimento de multisigs ou validadores

A segurança **não é herdada automaticamente do Ethereum**.

---

### Rollup
Solução de escalabilidade Layer 2 onde:
- transações são executadas fora do Ethereum
- mas o estado e a verificação final dependem do Ethereum L1

Rollups **não são blockchains soberanas**.
Eles herdam segurança diretamente do Ethereum.

---

### Optimistic Rollup
Tipo de rollup que assume que transações são válidas por padrão.
Características:
- permite desafios (fraud proofs)
- possui período de contestação
- saques têm delay

Exemplos: Optimism, Arbitrum.

---

### ZK Rollup
Tipo de rollup que utiliza provas criptográficas de validade (zero-knowledge proofs).
Características:
- cada lote de transações vem com uma prova matemática
- validade imediata no Ethereum
- maior complexidade técnica

Exemplos: zkSync, Starknet.

---

### Herança de Segurança
Rollups herdam segurança do Ethereum porque:
- qualquer estado inválido pode ser provado on-chain
- o Ethereum é o árbitro final

Bridges **não herdam** essa segurança automaticamente.

---

### Comparação Conceitual

Bridges:
- conectam blockchains independentes
- exigem confiança adicional
- maior risco sistêmico

Rollups:
- escalam o Ethereum
- não exigem confiança no operador
- segurança baseada em provas e L1

---

### Frase-chave
Bridges movem valor entre soberanias.
Rollups escalam a mesma soberania.
---

## 💰 9) Tópicos gerais: O que é MATIC?
- Era o token nativo da Polygon PoS  
- Hoje, migrado para **POL**  
- Funções:
  - pagar taxas  
  - staking/validação  
  - governança  
- Papel semelhante ao ETH no Ethereum

---

## 🏦 10) Tópicos gerais: O que é escrow?
- “Cofre inteligente” com regras para liberar fundos  
- Exs.:
  - libera dinheiro quando objetivo for atingido  
  - devolve fundos se o prazo expirar  
- Na blockchain:
  - é simplesmente um smart contract que controla saldo e condições

---

## 🧬 11) Tópicos gerais: O que é um contrato “Factory”?
- Contrato que cria outros contratos
- Motivos:
  - padronizar deploys  
  - criar um contrato por projeto  
  - endereços previsíveis  
  - reduzir complexidade  
- Factory → cria → Project / Escrow / etc.  
- “Deployed contract” = contrato efetivamente criado na rede

---

## 🪙 12) Tópicos gerais: O que é um token ERC-20?
- Padrão de tokens fungíveis no Ethereum
- Deve ter:
  - `balanceOf`
  - `transfer`
  - `approve`
  - `transferFrom`
  - eventos
- Exemplos: MATIC, USDT, USDC, AAVE

---

## 🗳️ 13) Tópicos gerais: O que são módulos de votação (governance modules)?
- **Governor:** cria propostas e votações  
- **Timelock:** executa decisões após X horas/dias  
- **Voting Token:** define peso de voto  
- Implementações prontas no **OpenZeppelin**

---

## 🔍 14) Tópicos gerais: O que são serviços off-chain? Eles podem ser manipulados?
### Exemplos:
- The Graph (indexador)
- Servidores da empresa
- Oráculos como Chainlink

### Riscos:
- serviços off-chain podem ser manipulados  
- smart contracts críticos não devem depender deles diretamente  

### Boas práticas:
- decisões financeiras = apenas dados on-chain  
- se precisar de externos → oráculos descentralizados  
- manter verificabilidade

---

## 🛡️ 15) Tópicos gerais: O que é usar o OpenZeppelin para padrões?
- Biblioteca com contratos auditados:
  - ERC-20  
  - ERC-721  
  - Governor  
  - Timelock  
  - AccessControl  
  - Pausable  
  - Ownable  
  - Upgrades  
- Equivale a usar classes-base no Django em vez de escrever tudo do zero

# Tópicos gerais:🔐 Proof of Stake, Incentivos e Segurança no Ethereum

## Tópicos gerais:🧠 Proof of Stake (PoS)

- Mecanismo de consenso onde a segurança da rede é garantida por **capital em risco** (ETH em stake)
- Substitui o gasto energético do Proof of Work
- Validadores:
  - bloqueiam ETH para participar
  - são recompensados por comportamento correto
  - são punidos por comportamento malicioso ou incorreto

👉 Segurança vem de risco econômico, não de confiança.

---

## Tópicos gerais:💰 Stake

- Quantidade de ETH bloqueada por um validador para participar do consenso
- No Ethereum:
  - **32 ETH = 1 validador**
- O stake:
  - **não mede mérito**
  - **não mede reputação**
  - mede exclusivamente **risco econômico**

---

## Tópicos gerais:👤 Validador

Participante do protocolo que:
- propõe blocos (quando selecionado)
- valida blocos propostos por outros
- emite **attestations** (votos)

Importante:
- o validador não decide “o que é certo”
- ele apenas verifica se **regras objetivas** foram seguidas

---

## Tópicos gerais:🧾 Attestation

- Assinatura criptográfica emitida por um validador indicando que:
  - um bloco é válido segundo as regras do protocolo
  - aquele bloco deve ser considerado na escolha da cadeia
- Cada attestation tem peso proporcional ao ETH em stake do validador

---

## Tópicos gerais:⚖️ Peso de voto (Stake-weighted voting)

No PoS do Ethereum:
- não existe “1 pessoa = 1 voto”
- votos são ponderados pelo ETH em stake
- mais ETH corretamente bloqueado → maior peso no consenso

👉 O consenso reflete **apoio econômico**, não opinião.

---

## Tópicos gerais:🌿 Fork-choice rule

- Algoritmo que decide qual cadeia seguir quando existem múltiplos forks válidos
- No Ethereum:
  - soma o peso das attestations
  - escolhe o fork com maior apoio econômico

Importante:
- o fork-choice é **dinâmico**
- pode mudar conforme novas attestations chegam

---

## Tópicos gerais:🔒 Finality (Casper FFG)

- Mecanismo que define quando um bloco se torna **irreversível**
- Quando um bloco é finalizado:
  - revertê-lo exige violar regras explícitas
  - implica perda massiva de ETH em stake
  - o ataque é detectável e punível

👉 Finality transforma consenso probabilístico em **segurança forte**.

---

## Tópicos gerais:✂️ Slashing

- Penalidade severa aplicada quando um validador:
  - vota de forma conflitante (double vote)
  - apoia forks incompatíveis
  - propõe ou valida blocos inválidos de forma comprovável

Consequências:
- parte do ETH em stake é destruída
- em casos graves, o validador é expulso do conjunto

👉 Slashing é o principal mecanismo de dissuasão no PoS.

---

## Tópicos gerais:❌ “Votar errado” (no contexto do PoS)

Não significa:
- julgar transações “boas” ou “más”

Significa:
- violar regras formais do consenso
- assinar mensagens conflitantes
- apoiar blocos tecnicamente inválidos

👉 É um erro **objetivo e verificável**, não interpretativo.

---

## Tópicos gerais:💣 Risco econômico

No PoS:
- segurança não vem de confiança
- vem de risco financeiro explícito

O validador:
- ganha pequenas recompensas por agir corretamente
- corre risco de grandes perdas ao tentar desviar

👉 O sistema assume **atores racionais**, não atores honestos.

---

## Tópicos gerais:🎯 Incentive Design (Design de Incentivos)

- Arquitetura que alinha:
  - comportamento individual
  - segurança coletiva da rede

No Ethereum PoS:
- seguir as regras é economicamente racional
- atacar a rede é economicamente autodestrutivo

---

## Tópicos gerais:🔄 PoW vs PoS — Comparação de Segurança

### Proof of Work (PoW)
- custo: energia + hardware
- ataque: gastar mais eletricidade
- capital pode ser reaproveitado fora da rede

### Proof of Stake (PoS)
- custo: capital bloqueado
- ataque: perder o próprio ETH
- capital está preso e visível on-chain

👉 Ambos convertem segurança em custo, mas por mecanismos diferentes.

---

## Tópicos gerais:🏦 Concentração de poder no PoS

- PoS favorece quem tem mais capital:
  - mais ETH → mais validadores → mais peso

Freios existentes:
- limite técnico por validador (32 ETH)
- slashing escala com o capital
- pressão social e governança fora do protocolo

👉 O protocolo não garante descentralização econômica, apenas a torna mensurável.

---

## Tópicos gerais:🤝 Confiança vs Risco

- O Ethereum PoS:
  - não exige confiar nos validadores
  - exige apenas que ajam racionalmente sob risco financeiro

👉 Confiança social é substituída por **incentivos econômicos explícitos**.

---
# Transição Web2 → Web3 — Fundamentos e Arquitetura Mental

## 🧠 CAMADA 1 — Mudar o modelo mental (fundamental)

### Transição Web2 → Web3: 🔴 Diferença central entre Web2 e Web3

**Web2**
- código pode mudar
- bugs são corrigíveis
- banco de dados é mutável
- acesso é controlado por uma entidade

**Web3**
- contratos não podem mudar (na prática)
- bugs custam dinheiro real
- estado é público e imutável
- depois do deploy, ninguém “manda”

👉 Isso muda completamente:
- arquitetura
- estratégia de testes
- responsabilidade
- necessidade de paranoia saudável

---

### Transição Web2 → Web3: 📦 O que realmente é um smart contract

- Um smart contract **não é um backend**
- Ele é:
  - um programa determinístico
  - rodando em milhares de máquinas
  - com custo por instrução (gas)
  - sem acesso externo
  - sem IO
  - sem relógio confiável
  - sem threads
  - sem exceptions no sentido tradicional

**Analogia correta:**
- Uma *stored procedure*:
  - distribuída
  - imutável
  - pública
  - paga por uso
  - irreversível

---

## Transição Web2 → Web3: 🧩 CAMADA 2 — Base técnica mínima (para não ficar boiando)

Aqui o objetivo não é virar especialista, mas ganhar **vocabulário operacional**.

---

### Transição Web2 → Web3: ⚙️ 1️⃣ EVM de verdade

Estudar:
- o que é a EVM
- stack machine
- gas
- storage vs memory vs calldata
- opcodes (conceito, não decorar)

Você precisa entender por que:
- loops são perigosos
- arrays grandes são caros
- leitura e escrita têm custos diferentes

👉 Isso evita escrever contratos ruins sem perceber.

---

### Transição Web2 → Web3: 🧑‍💻 2️⃣ Solidity como linguagem restrita

Solidity **não é JavaScript**.

É uma linguagem:
- com tipagem forte
- focada em estado persistente
- com semântica própria de memória
- cheia de riscos específicos

Conceitos essenciais:
- `msg.sender`, `msg.value`
- `call`, `delegatecall`
- modifiers
- events
- visibilidade (`public`, `external`, `internal`, `private`)
- herança (muito usada)
- riscos clássicos:
  - reentrancy
  - overflow
  - underflow
  - storage collision

---

### Transição Web2 → Web3: 📜 3️⃣ ERCs como protocolos sociais

ERCs **não são bibliotecas**.
São acordos sociais codificados.

Estudar:
- ERC-20
- ERC-721
- allowance model
- snapshots

Entender:
- por que eles existem
- quais ataques exploraram implementações ruins
- como pequenos desvios do padrão causam perdas reais

---

## Transição Web2 → Web3: 🛠️ CAMADA 3 — Toolchain (onde tudo começa a fazer sentido)

Aqui a maioria se perde — organização é crucial.

---

### Transição Web2 → Web3: 🧪 Hardhat (ou Foundry)

É o seu:
- ambiente local
- test runner
- deployer
- debugger

Você vai:
- rodar blockchain local
- simular ataques
- fazer fork da mainnet
- escrever testes antes do deploy

👉 Em Web3, quem não testa, **perde dinheiro**.

---

### Transição Web2 → Web3: 🔌 ethers.js

É:
- a ponte entre frontend e contratos
- base de scripts de deploy
- usada em automações off-chain

Você precisa entender:
- como instanciar contratos
- como chamar funções
- diferença entre:
  - `call`
  - `sendTransaction`

---

### Transição Web2 → Web3: 🌐 RPC + Nodes (na prática)

Você **não fala com a blockchain**.
Você fala com um **node via RPC**.

Infura / Alchemy:
- abstraem infraestrutura pesada
- são pontos de confiança

Você precisa saber:
- quando confiar
- quando rodar node próprio
- quando usar múltiplos providers

---

## Transição Web2 → Web3: 🏗️ CAMADA 4 — Arquitetura de projetos reais

Aqui está o objetivo final.

---

### Transição Web2 → Web3: 🧱 Padrões de arquitetura on-chain

- Factory contracts
- Escrow por projeto
- Governor + Timelock
- Multisig admin
- Upgradeability vs Imutabilidade

Aqui entram decisões:
- técnicas
- sociais
- éticas

**Exemplo:**
- permitir upgrade → menos risco técnico
- não permitir upgrade → mais confiança social

---

### Transição Web2 → Web3: 🧠 Governança ≠ CRUD

Governança envolve:
- poder
- incentivos
- ataques econômicos

Você precisa entender:
- quorum
- snapshot
- time delay
- stake vs vote

E principalmente:
- como pessoas abusam do sistema
- mesmo quando o código está “correto”

---

### Transição Web2 → Web3: 🔍 Off-chain sem trair o on-chain

Serviços off-chain:
- leem
- indexam
- exibem
- notificam

Eles **não decidem nada crítico**.

👉 Decisão financeira **sempre on-chain**.

---
# 📚 Como estudar isso de forma eficaz (método, não links):
## Fase 1 — Fundamentos práticos

### Ler docs Ethereum + Polygon

## 🧭 Guia de Estudos — Base Técnica Web3 (Ethereum + Polygon)

> Objetivo:
> Construir base técnica sólida para compreender e desenvolver projetos Web3
> (smart contracts, arquitetura on-chain/off-chain, governança e segurança),
> partindo do zero prático até um mini-projeto com padrões da indústria.

---

## 🔴 BLOCO 1 — Fundamentos de Blockchain & Ethereum (Obrigatório)

### Conceitos gerais
- [x] O que é uma blockchain (revisão técnica)
- [x] Diferença entre Web2 e Web3 (modelo mental)
- [x] Imutabilidade e consenso
- [x] Estado global da blockchain

### Contas e transações
- [ ] EOA (Externally Owned Accounts)
- [ ] Contract Accounts
- [ ] Transações:
  - [ ] nonce
  - [ ] gas
  - [ ] gas limit
  - [ ] gas price / base fee
- [ ] O que acontece quando uma transação é enviada

🎯 Objetivo do bloco:
> Conseguir explicar, passo a passo, o que acontece quando alguém chama uma função
> de um contrato na blockchain.

---

## 🔴 BLOCO 2 — Smart Contracts (Modelo Mental Correto)

- [ ] O que é um smart contract (tecnicamente)
- [ ] Diferença entre:
  - [ ] call (leitura)
  - [ ] transaction (escrita)
- [ ] Determinismo
- [ ] Por que contratos não:
  - [ ] acessam internet
  - [ ] acessam arquivos
  - [ ] acessam tempo real confiável
- [ ] Como contratos chamam outros contratos
- [ ] Eventos (logs) e seu papel

🎯 Objetivo do bloco:
> Entender **limitações e garantias**, não apenas possibilidades.

---

## 🔴 BLOCO 3 — EVM (Ethereum Virtual Machine)

### Funcionamento interno (nível correto)
- [ ] O que é a EVM
- [ ] Máquina baseada em stack (conceito)
- [ ] Execução determinística
- [ ] Gas como custo computacional

### Memória e armazenamento
- [ ] `storage` (persistente)
- [ ] `memory` (temporário)
- [ ] `calldata` (somente leitura)
- [ ] Diferença de custo entre leitura e escrita

### Armadilhas comuns
- [ ] Por que loops são perigosos
- [ ] Por que arrays grandes custam caro
- [ ] O que significa “bricking” um contrato

🎯 Objetivo do bloco:
> Não escrever código ineficiente ou perigoso sem perceber.

---

## 🔴 BLOCO 4 — Solidity (Essencial antes de codar)

### Base da linguagem
- [ ] Tipos básicos
- [ ] Funções
- [ ] Construtor
- [ ] Visibilidade:
  - [ ] public
  - [ ] external
  - [ ] internal
  - [ ] private

### Contexto de execução
- [ ] `msg.sender`
- [ ] `msg.value`
- [ ] `address(this)`
- [ ] `block.number` (conceito, cuidado)

### Controle e segurança básica
- [ ] `require`
- [ ] `revert`
- [ ] `error`
- [ ] Modifiers
- [ ] Events

🚫 Fora de escopo por enquanto:
- Inline assembly
- Yul
- ABI encoding profundo
- Otimizações avançadas

🎯 Objetivo do bloco:
> Ser capaz de ler e escrever contratos simples com clareza.

---

## 🔴 BLOCO 5 — Tokens & Padrões (ERCs)

### Conceitos
- [ ] O que é um token fungível
- [ ] Por que tokens são contratos
- [ ] Diferença entre token e moeda nativa

### ERC-20
- [ ] O que é o padrão ERC-20
- [ ] Funções principais:
  - [ ] balanceOf
  - [ ] transfer
  - [ ] approve
  - [ ] transferFrom
- [ ] Allowance model
- [ ] Riscos e armadilhas comuns

🎯 Objetivo do bloco:
> Entender tokens como **infraestrutura padrão**, não como “moedas”.

---

## 🔴 BLOCO 6 — Polygon (Visão Geral, sem aprofundar)

- [ ] O que é a Polygon
- [ ] Polygon PoS (sidechain)
- [ ] Diferença entre Polygon e Ethereum
- [ ] Taxas (gas)
- [ ] MATIC / POL
- [ ] Bridge (conceito geral)

🚫 Ignorar por enquanto:
- zkEVM
- CDK
- Appchains
- Soluções enterprise

🎯 Objetivo do bloco:
> Saber **onde** você está deployando e **por que** usar Polygon.

---

## 🔴 BLOCO 7 — Infraestrutura Básica (Conceitual)

- [ ] O que é um node
- [ ] O que é RPC
- [ ] O papel de Infura / Alchemy / QuickNode
- [ ] Diferença entre rodar node próprio e usar provider
- [ ] O que são serviços off-chain
- [ ] O que eles **podem** e **não podem** fazer

🎯 Objetivo do bloco:
> Entender a fronteira entre on-chain e off-chain.

---

⚠️ Só avançar depois de completar os blocos anteriores.
- Escrever contratos simples
- [ ] Hardhat / Foundry
- [ ] Testes de smart contracts
- [ ] Primeiro contrato simples
- [ ] Deploy em testnet
- [ ] Frontend mínimo
- [ ] Escrow básico
- [ ] Factory contracts
- [ ] Governança
- Quebrar eles de propósito

- Entender erros comuns

### Fase 2 — Segurança
- [ ] Segurança avançada

- Estudar hacks reais

- Entender por que aconteceram

- Simular ataques em testes

### Fase 3 — Mini-projeto

- Escrow simples

- Token ERC-20

- Factory

- Frontend mínimo

- Deploy em testnet

### Fase 4 — Refinamento

- Melhorar arquitetura

- Adicionar governança

- Escrever README técnico

- Pensar como auditor
---
# 📚 Documentação essencial — Como usar sem se perder

## 🔹 1) Polygon Docs  
https://docs.polygon.technology/

👉 **Bom, mas perigoso para iniciantes técnicos**

Esse conjunto de docs é:
- extremamente completo
- muito amplo
- escrito para vários perfis:
  - infraestrutura
  - zk
  - DeFi
  - enterprise

📌 Use para:
- entender o ecossistema Polygon
- saber o que existe
- diferenciar:
  - Polygon PoS
  - zkEVM
  - CDK
  - bridges

🚫 Não use como sequência de aprendizado linear  
Esses docs **não foram feitos para isso**.

---

## 🔹 2) Ethereum Developers Docs  
https://ethereum.org/developers/docs/

👉 **Esse é o seu “docs raiz”**

- Melhor material conceitual-técnico existente hoje
- Base real de entendimento do ecossistema

📌 Use para:
- entender a EVM
- entender contas, transações e gas
- entender smart contracts como sistema

👍 É estruturado, mas:
- não é didático no sentido tradicional
- funciona como **referência profunda**

---

## 🔹 3) Solidity Documentation  
https://docs.soliditylang.org/en/v0.8.31/

👉 **Manual da linguagem, não curso**

📌 Use para:
- consultar sintaxe
- entender:
  - tipos
  - visibilidade
  - memória
- confirmar comportamentos específicos

🚫 Não tente “aprender Solidity” lendo isso do começo ao fim  
Vai ser improdutivo e frustrante.

---

## 🔹 4) Ethereum Development Docs (eth-develop)  
https://eth-develop.readthedocs.io/

👉 **Subestimado e bom**

Apesar de mais antigo:
- é mais direto
- tem menos marketing
- foca mais em engenharia “raiz”

📌 Bom para:
- criar base mental inicial
- entender conceitos sem ruído

---

## 🔑 2️⃣ Documentações adicionais recomendadas

Essas complementam muito bem as oficiais.

---

## 🔑 A) OpenZeppelin Learn  
https://docs.openzeppelin.com/learn/

👉 **Isso aqui é ouro**

Por quê?
- conecta Solidity + segurança + padrões
- explica *por que* as coisas são feitas
- mostra armadilhas reais de produção

📌 Se você ler apenas **um material além dos oficiais**, que seja este.

---

## 🔑 B) Ethereum Yellow Paper (opcional, seletivo)

👉 Não é para ler inteiro

Use para:
- entender o papel formal da EVM
- saber que existe uma especificação matemática da rede

📌 Serve para consulta pontual, não estudo linear.

---

## 🔑 C) Hardhat Docs (mais tarde)  
https://hardhat.org/docs

👉 **Não agora**

📌 Use somente quando:
- você estiver prestes a escrever contratos
- já entender EVM + Solidity básico

Antes disso, vira ruído.

---
<!-- TODO: Perguntas que preciso responder-->
# Perguntas que preciso responder

---












<!-- TODO: coisas para conferir e fazer perguntas -->

# Coisas para conferir e fazer perguntas
6) Fluxo de desenvolvimento prático (passo a passo para um PoC)

Design de contratos (diagramas + invariants): Escrow, ProposalFactory, VotingToken, Governance.

Escrever contratos em Solidity (usar OpenZeppelin para padrões).

Testes locais com Hardhat/Foundry: unit, property tests, fuzzing, fork mainnet tests.

Deploy em testnet (Mumbai) e testes end-to-end com wallets reais (MetaMask). 
docs.polygon.technology

Auditoria/peer review (ao menos internal audit + bug bounty antes do mainnet).

Observability: indexador (The Graph / custom), dashboards de events e alertas.

Governança e processos operacionais: multisig, timelocks, playbooks para emergência.

7) Ferramentas e recursos essenciais para estudar/praticar

Docs oficiais Polygon (PoS, zkEVM, Portal) — começar aqui. 
polygon.technology
+2
docs.polygon.technology
+2

Hardhat / Foundry — ambientes de desenvolvimento. 
docs.polygon.technology

OpenZeppelin contracts & guides (governance patterns, security). 
OpenZeppelin

Artigos e guidelines de segurança (papers, guias de auditoria/formal verification). 
ScienceDirect
+1

Bridges & Portal docs — para mover ativos/UX de onboarding. 
docs.polygon.technology
+1

8) Pontos de tomada de decisão que você deve considerar (sérios)

Onde guardar controle: contratos imutáveis ou proxy upgradable? Imutável = mais confiança pública; proxy = correção de bugs, mas exige governança forte.

On-chain vs off-chain voting: on-chain (transparente, caro); off-chain + execução on-chain (Snapshot + Timelock) = economia + riscos menores de custo.

Vesting / tranches: liberar tudo ao recebedor na meta alcançada vs liberar por milestones com oráculos de verificação/relatórios.

Quem pode propor? aberto a qualquer recebedor ou só vetted projects? Isso muda ataques de spam e custo operacional.

9) Exemplo de invariantes (coisas para testar/assegurar)

Escrow.balance >= sum(deposits) − withdrawals.

Só liberar fundos quando totalDeposited >= goal && now <= deadline (ou outra lógica definida).

Votação: votos contados com snapshot at block X; evitar double vote.

10) Próximos passos práticos (se quiser eu executo)

Posso:

gerar um esqueleto de contratos (Factory + Escrow + Token) em Solidity com Hardhat config e exemplos de teste;

ou preparar um roteiro de estudo com links diretos, exercícios e desafios práticos (do tipo: deploy no Mumbai, criar frontend simples com ethers.js).

Antes de eu colocar a mão na massa, me responde rapidinho (essas perguntas vão me deixar plantar um plano ou PoC técnico muito mais útil):

Você quer um PoC funcional (deploy em testnet + frontend) ou apenas material de estudo/arquitetura?

Preferência por zkEVM (mais “futuro”, custos e segurança diferentes) ou Polygon PoS / sidechain (mais barato e mais usado hoje)?

Quer on-chain voting estritamente ou off-chain (Snapshot) com execução on-chain?

Tem preferência por ferramentas (Hardhat vs Foundry) ou quer que eu escolha a stack padrão (Hardhat + ethers)?

Diz aí e eu já te entrego: (A) um esqueleto de contratos + testes, ou (B) roteiro de aprendizado com exercícios práticos e checklists de segurança — ou ambos.
