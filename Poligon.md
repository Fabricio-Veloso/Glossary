# Glossário de Polygon

## Sumário:

1. Tópicos gerais:
2. Transição Web2 → Web3
3. 📚 Como estudar isso de forma eficaz (método, não links):

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
### Fase 1 — Fundamentos práticos

- Ler docs Ethereum + Polygon

- Escrever contratos simples

- Quebrar eles de propósito

- Entender erros comuns

### Fase 2 — Segurança

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
