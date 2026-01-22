# Glossário de WEB3

## Sumário:
(faça uma busca por qualquer um desses termos na lista abaixo para encontra-los em seus respectivos lugares).
- Tópicos gerais.
    - O que é uma sidechain?
    - O que são appchains?
    - O que são SDKs no contexto de desenvoldimento de ETH ?
    - O que é compatibilidade EVM?
    - Solidity e Vyper são linguagens completas?
    - Diferença entre infra e infra on-chain.
    - O que são nodes / RPCs?
    - O que são nodes / RPCs?
    - O que são relayers e bridges?
    - O que é MATIC?
    - O que é escrow?
    - O que é um contrato “Factory”?
    - O que é um token ERC-20?
    - O que são módulos de votação (governance modules)?
    - O que são serviços off-chain? Eles podem ser manipulados?
    - O que é usar o OpenZeppelin para padrões?
    - Proof of Stake (PoS).
    - Stake.
    - Validador.
    - Attestation.
    - Peso de voto (Stake-weighted voting).
    - Fork-choice rule.
    - Finality (Casper FFG).
    - Tópicos gerais:✂️ Slashing.
    - “Votar errado” (no contexto do PoS).
    - Tópicos gerais:💣 Risco econômico.
    - Incentive Design (Design de Incentivos).
    - PoW vs PoS — Comparação de Segurança.
    - Concentração de poder no PoS
    - Confiança vs Risco
    - Assinatura, encoding e envio de transações no Ethereum
    - Tópicos Gerais: RLP (Recursive Length Prefix).
    - Caminho completo de uma transação (visão geral).

---

- Tópicos Práticos.
  - Tópicos Práticos: 🧱 Uso de `require`.
    - O que é `require`, de verdade (nível EVM) 
    - require vs revert vs assert
    - Regras práticas de uso do require
    - Por que contratos seguros usam tanto require
    - Exemplos — bom vs ruim
    - Checklist mental simples antes de usar require
  - Uso de \`events\` em Solidity — Observabilidade, Histórico e Semântica.
    - O que events são na prática (sem romantizar)
    - Quando usar events (regra simples)
    - Aplicando events em um Counter
    - 🔥Emitindo events (parte prática)
    - Como isso é usado fora do contrato (visão prática)
    - Checkpoint mental - diferenças entre storage e Events
    - emit pode ser usado para outras coisas? (não)
        - O que `emit` faz exatamente
        - O que NÃO existe (no contexto de emit) 
        - recaptulação para "emit"  
    - Precisa declarar um event antes de usar `emit`?
        - Por que isso é obrigatório?
        - Analogia rápida com funções comuns
        - Regra mental final 
  - (EVM context) Coisas que existem em todo contrato.
      - Principais “variáveis globais” (as mais importantes)
        - 🔹 `msg`
        - 🔹 `address(this)`
        - 🔹 `block`
        - 🔹 `tx`
    - Regras especiais sobre `address` e `.balance`
        - Um contrato recebe ETH se
        - Enviar ETH (atualmente se usa call)
        - Como mudar o owner do contrato (padrão real)
        - `public`, `external`, `internal`, `private` (sem confusão)
  - 🧠 Checkpoint geral 
  - Tópicos Práticos: `Indexed`.
    - 🔹 Topics (índice)
    - Data (payload)
    - O que muda quando você marca algo como indexed
    - Limites e regras importantes para indexadores
        - ⚠️ Limite duro
        - ⚠️ Tipos grandes
    - Quando usar indexed
    - Quando NÃO usar indexed
    - Custo de gás de Indexed
    - Regras práticas pra uso de Indexed
  - Tópicos Práticos: `modifier`.
    - O que é um modifier (conceitualmente)
    - Sintaxe básica (sem mágica)
    - Usando o modifier na prática
    - Aplicando em um contrato Counter
    - Modifier pode receber parâmetros? ✅ Sim
    - Modifier pode rodar código depois da função?
    - Boas práticas reais (importante)
    - ligando com o que você já sabe
    - Modifiers, require e custom errors — desmistificando o uso correto
        - Contexto da Dúvida (posso usar com require e custom errors?)
        - Resposta curta (sim) 
    - ABI Encoding.
        - O que é ABI encoding
        - A EVM não entende “funções”, “strings” ou “eventos” (são apenas abstrações)
        - ABI Encoding na ENTRADA do contrato (call data)
        - ABI Encoding na SAÍDA do contrato (return data)
        - ABI Encoding em ERROS (revert)
        - ABI Encoding em Custom Errors
        - ABI Encoding em `require("string")`
        - ABI Encoding em EVENTS (logs)
        - Um modelo mental unificado (direções, EVM só carrega bytes, ABI da semântica )
        - Por que isso importa para escrever e auditar contratos (ABI é design de API)
        - Uma provocação (Se você entendeu ABI, consegue contruir tudo apartir apenas dele)
        - “Todos os encodings usam selector de 4 bytes e o resto 32? E tudo vem de hashes?”
            - 🔹 1.1 O que é hash de verdade no ABI?
            - 🔹 1.2 O que **NÃO** vem de hash
            - 🔹 1.3 Por que tudo “parece hash”?
            - Então por que 32 bytes?
        - “O encoding é tipo uma tabela nome → valor?”
        - Como pensar no ABI Encoding corretamente
        - os tipos dinâmicos? (ABI vira layout de memória)
        - Resumo técnico das regras fundamentais
        - Resumo técnico das regras fundamentais
            - 🔹 Identificação
            - 🔹 Dados
        - Um teste mental (bom sinal se você conseguir responder)
        - A regra real do ABI (O ABI é definido por tipo + ordem)
            - Onde isso aparece de forma concreta
            - 🔹 1. Function selector
            - 🔹 2. Decodificação off-chain
            - Um exemplo mental forte
            - Então o que exatamente muda no ABI?
            - Onde isso aparece no Hardhat (concreto)
            - Comparação real (mental)
            - Onde isso é usado nos testes
        - Importante: ABI ≠ Solidity
        - Gerando call data com ethers (efeito antes da descrição)
        - O ponto exato onde isso acontece
        - Gerando call data manualmente
        - O ponto CRÍTICO do modelo mental
        - Observação importante
        - E quando você usa counter.add(5)?
  - Tópicos Práticos: Custom errors
    - Contexto da dúvida (custom errors é "apenas declarar `error Nome();` e depois dar `revert Nome();`?")
    - A sintaxe básica (sem truque escondido)
        - Então por que custom errors existem? (o problema real)
            - 🔴Gas e bytecode
            - 🔴Semântica fraca com string
        - Custom errors podem (e devem) ter parâmetros
        - Onde declarar custom errors (escopo importa)
        - Require vs revert + custom error
        - Pegadinhas importantes (herança e nomes)
        - ⚠️ 1. Errors não são herdados magicamente
        - ⚠️ 2. O nome do erro importa MUITO
        - ⚠️ 3. Custom error não é exceção “high-level”
        - Quando NÃO usar custom errors
        - Gas e bytecode — impacto real (Hardhat comparando uso de gás de dois contratos equivalentes)
        - Custom errors fazem parte da ABI pública
        - Error como API (analogia útil)
        - Checklist mental rápido (perguntas para se fazer antes de escrever um error)
        - Custom errors Conclusão prática
        - “Projetar todos os erros antes” — o que isso realmente significa
            - 🔹 O que faz muito sentido projetar antes
            - 🔹 O que NÃO faz sentido congelar cedo demais
        - “Evitar `require` então é sempre melhor?”
        - O ganho real de se usar custom errors 
            - Aplicando em um Counter mínimo 
            - 📌 Requisitos do sistema (antes do código)
            - 🧱 Projeção de erros (primeiro!)
            - 🧩 Implementação do contrato
            - O que esse exemplo prova
            - Insight mais valioso (guarda esse)
        - Versionamento e breaking changes (entrada)
        - O que é breaking change em contratos 
        - Por que errors quebram compatibilidade
        - 🔴 Mudanças que quebram ABI
        - Exemplo concreto: Counter v1 → v2 (quebrando tudo)
            - Versão “profissional” de v2 (compatível)
            - 🟢 Estratégia A — Manter o erro antigo
            - 🟡 Estratégia B — Introduzir novo erro sem remover o antigo
            - 🔴 Estratégia C — Quebrar explicitamente (major version)
        - Regras práticas para versionar errors (guarda isso)
            - ✔️ 1. Erros públicos são quase imutáveis
            - ✔️ 2. Nome importa mais que mensagem
            - ✔️ 3. Parâmetros também fazem parte do contrato
            - ✔️ 4. Agrupe errors como API
            - Como um auditor enxerga isso
        - O insight final (muito importante)
        - Próximo passo natural 
        - Testando, protegendo e versionando custom errors no hardhat (nível metal)
        - Exemplo com o counter
            - Testando parâmetros do error
            - Validando selectors explicitamente (nível auditor)
            - Detectando breaking change automaticamente
            - Micro-workflow técnico saudável (curto e prático)
            - O que muda na sua cabeça depois disso
            - Um detalhe que pouca gente usa (você pode criar um teste **só para abi**)
        - Próximo passo (quais erros são públicos e quais são internos, como evoluir o protocolo)
        - 
---



- Transição Web2 → Web3.
- Como estudar isso de forma eficaz (método, não links).
- Documentação essencial — Como usar sem se perder.

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

## 🧩 3) Tópicos gerais: O que são SDKs no contexto de desenvoldimento de ETH ?
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
#  Tópicos gerais: Assinatura, encoding e envio de transações no Ethereum

## Assinatura de transações
No Ethereum, uma transação **não é criptografada**, ela é **assinada**.  
Assinar significa gerar uma prova criptográfica de que o emissor possui a chave privada correspondente ao endereço `from`.

A assinatura é feita sobre o **hash do conteúdo da transação**, e não sobre o JSON em si.  
Esse hash é obtido aplicando `keccak256` sobre a transação codificada (RLP), **sem os campos de assinatura**.

A assinatura gera três valores:
- `r`
- `s`
- `v`

Esses campos permitem que qualquer nó da rede:
- recupere a chave pública do emissor
- derive o endereço
- verifique que a transação foi realmente autorizada por aquele endereço

---

## “Conteúdo embaralhado” (raw transaction)
O campo `raw` retornado por um nó RPC **não está criptografado**.  
Ele é uma **representação hexadecimal de bytes binários**, resultado de:

1. Encoding eficiente da transação (RLP)
2. Inclusão da assinatura (`v`, `r`, `s`)
3. Serialização final para transporte

O conteúdo parece “embaralhado” porque:
- não é texto
- não é JSON
- não é estruturado para leitura humana

Qualquer nó pode decodificar esse conteúdo e validar a transação.

---

## Assinatura ≠ criptografia
É fundamental não confundir os conceitos:
- **Assinatura** garante autenticidade e integridade
- **Criptografia** garantiria confidencialidade (o que Ethereum não faz)

Todas as transações do Ethereum são públicas e legíveis por qualquer pessoa.

---

## Encoding eficiente
Antes de ser assinada e enviada, a transação precisa ser convertida de uma estrutura lógica (campos como `nonce`, `to`, `value`, etc.) para uma forma **binária compacta e determinística**.

O Ethereum usa **RLP (Recursive Length Prefix)** como esquema de encoding.

O objetivo do encoding eficiente é:
- reduzir o número de bytes transmitidos
- garantir parsing rápido e previsível
- evitar ambiguidades
- permitir hashing determinístico

---

## Tópicos Gerais: RLP (Recursive Length Prefix)
RLP é um método de encoding binário usado pelo Ethereum para:
- transações
- blocos
- estruturas internas do protocolo

Características principais:
- não depende de chaves ou criptografia
- codifica strings, inteiros e listas
- sempre produz a mesma saída para a mesma entrada
- inclui informações de tamanho no próprio encoding

RLP descreve apenas **estrutura**, não semântica.

---

## Hexadecimal como representação
Os dados da transação circulam na rede como **bytes**.  
A forma hexadecimal existe apenas para:
- visualização
- debug
- transporte em interfaces humanas (RPC, logs, explorers)

Hexadecimal **não é o encoding**, apenas a representação dos bytes já codificados.

---

## Por que JSON não é usado no protocolo
JSON é utilizado apenas na camada de interface (RPC), pois:
- é legível por humanos
- é fácil de debugar

Porém, ele não é adequado para consenso porque:
- é verboso
- não é binário
- pode ser ambíguo
- não é determinístico por padrão

No nível do protocolo, JSON nunca é utilizado.

---

## Tópicos Gerais: Caminho completo de uma transação (visão geral)
1. O usuário cria uma transação via software off-chain (wallet)
2. A transação é codificada em RLP
3. O hash da transação codificada é gerado
4. O hash é assinado com a chave privada do emissor
5. A assinatura é anexada à transação
6. A transação é serializada em bytes
7. Os bytes são representados em hexadecimal (raw transaction)
8. O nó RPC faz o broadcast para a rede









---
# Tópicos Práticos

## Tópicos Práticos: 🧱 Uso de `require` 
*em Solidity — Validação, Segurança e Semântica*

---
### 🎯 Contexto geral

- `require` é uma das construções mais importantes de Solidity.  
Entender **bem** o que ele faz antes de sair alterando código evita bugs caros, estados inválidos e falhas de segurança.

- Ele não é um detalhe de sintaxe — é parte central do **modelo mental Web3**.


### O que é `require`, de verdade (nível EVM)

`require` **não é** um `if` especial.

Ele é uma **barreira de validade da execução**.

Quando você escreve:

```solidity
require(condition, "erro");
```

Você está declarando:

“Se essa condição não for verdadeira, cancele toda a execução desta chamada.”

📌 Tecnicamente, o que acontece:

- A EVM executa a instrução **REVERT**  
- Todo o estado é restaurado ao que era antes da chamada  
- Nenhuma variável de storage é alterada  
- Nenhum ETH é transferido  
- O gás não utilizado é devolvido  
- A mensagem de erro é propagada para quem chamou  

👉 Ou seja: é uma execução que nunca existiu, do ponto de vista do estado da blockchain.

---

### require vs revert vs assert

#### 🔹 require

Use quando:

- o erro pode acontecer legitimamente  
- depende de input do usuário  
- faz parte das regras normais do contrato  

Exemplos típicos:

```solidity
require(msg.sender == owner);
require(amount > 0);
require(balance[msg.sender] >= amount);
```

👉 É o mecanismo padrão de validação externa.

---

#### 🔹 revert

É equivalente a `require(false, "...")`, mas usado de forma mais explícita.

```solidity
if (x == 0) {
    revert("x cannot be zero");
}
```

Use quando:

- a lógica de erro é mais complexa  
- existem múltiplas condições  
- você quer sair no meio da função  

📌 Na prática, `require` cobre cerca de 90% dos casos.

---

#### 🔹 assert ⚠️

⚠️ **Não é para validação de input.**

Use apenas quando:

- algo nunca deveria falhar  
- indica bug interno  
- quebra de invariantes do contrato  

```solidity
assert(totalSupply >= balance[msg.sender]);
```

📌 Semântica importante:

- se um `assert` falha, o contrato é considerado bugado  
- historicamente, falhas de `assert` eram tratadas como erros graves  
- conceitualmente significa: “isso é impossível; se aconteceu, há um erro de programação”

---

###  Regras práticas de uso do require

Essas são as regras que realmente importam no dia a dia.



#### ✅ Regra 1 — Use require no início da função

```solidity
function withdraw(uint amount) public {
    require(amount > 0);
    require(balance[msg.sender] >= amount);

    balance[msg.sender] -= amount;
}
```

❌ Nunca faça:

```solidity
balance[msg.sender] -= amount;
require(balance[msg.sender] >= 0); // errado
```

📌 Valida primeiro, executa depois.

---

#### ✅ Regra 2 — Não use require para fluxo normal

❌ Errado:

```solidity
require(x > 0);
x--;
```

✔️ Melhor:

```solidity
if (x == 0) return;
x--;
```

👉 `require` é para condições inválidas, não para controle normal de fluxo.

---

### ✅ Regra 3 — Não esconda require no meio da função

❌ Ruim:

```solidity
x += 1;
require(msg.sender == owner);
```

✔️ Bom:

```solidity
require(msg.sender == owner);
x += 1;
```

📌 Isso evita efeitos colaterais antes de uma falha.

---

###  Por que contratos seguros usam tanto require

Porque ele garante três propriedades críticas:

🔒 **1. Estado consistente**  
Se algo falhar, nada muda.

⛽ **2. Eficiência de gás**  
O usuário não paga pelo que não foi executado.

🧠 **3. Código legível e auditável**  

Auditores leem contratos assim:

“Quais são as condições para essa função rodar?”

E essas condições estão claras no topo da função.

---

###  Exemplos — bom vs ruim

❌ **Ruim (mentalidade Web2)**

```solidity
function withdraw(uint amount) public {
    if (balance[msg.sender] < amount) {
        return;
    }
    balance[msg.sender] -= amount;
}
```

Problemas:

- falha silenciosa  
- difícil de debugar  
- comportamento ambíguo para quem chama  

---

✅ **Bom (mentalidade Solidity)**

```solidity
function withdraw(uint amount) public {
    require(balance[msg.sender] >= amount, "Insufficient balance");
    balance[msg.sender] -= amount;
}
```

👉 Erro explícito, estado consistente, sem ambiguidade.

---

###  Checklist mental simples antes de usar require

Antes de escrever um `require`, pergunte:

❓ Isso é uma regra do contrato?  
❓ Pode falhar por erro do usuário?  
❓ Se falhar, nada deve mudar?

👉 Se todas forem “sim” → `require`.

---

📌 **Nota final**

Entender `require` bem cedo muda completamente:

- como você estrutura funções  
- como você pensa em segurança  
- como você escreve código auditável  

É uma daquelas peças pequenas que sustentam contratos grandes e seguros.

---

## Tópicos Práticos:  Uso de `events` em Solidity — Observabilidade, Histórico e Semântica


###  O que events são na prática (sem romantizar)

`events\` **NÃO** servem para lógica interna do contrato.

Eles servem para:

- comunicar coisas para fora da blockchain  
- permitir que aplicações acompanhem o que aconteceu  
- criar histórico legível e indexável  

📌 Um `event\` é basicamente:

> “Ei mundo offchain, algo relevante aconteceu aqui”

Eles:

- **não alteram estado**  
- **não podem ser lidos por outros contratos**  
- são gravados em **logs**, não em **storage**  

👉 Ou seja: events existem **exclusivamente para observação externa**.

---

###  Quando usar events (regra simples)

Use `events\` quando:

- algo importante aconteceu  
- alguém mudou estado  
- alguém recebeu ou enviou valor  
- algo precisa ser observável fora da chain  

❌ **Não use events para**:

- controle de acesso  
- validações  
- lógica interna  
- substituto de storage  

📌 Se a informação é necessária **para o contrato decidir algo**, ela **não pode** ser um event.

---

###  Aplicando events em um Counter 

Vamos pensar como engenheiros, não como “quem segue tutorial”.

Pergunta correta:

> O que é relevante alguém saber olhando de fora?

Respostas óbvias:

- contador foi incrementado  
- contador foi decrementado  
- contador foi resetado  
- **quem** fez isso  
- **quanto** mudou  

---

#### ✍️ Definindo os events

```solidity
event Increment(address indexed by, uint256 amount, uint256 newValue);
event Decrement(address indexed by, uint256 amount, uint256 newValue);
event Reset(address indexed by);
```

📌 `indexed\` permite filtrar por endereço depois (extremamente comum).

👉 Cada `event\` descreve **um fato que aconteceu**, não uma regra.

---

### 🔥 Emitindo events (parte prática)

```solidity
function increment(uint256 amount) public {
    require(msg.sender == owner, "only the owner can increment");
    require(amount > 0, "amount must be greater than zero");

    count += amount;

    emit Increment(msg.sender, amount, count);
}
```

```solidity
function decrement(uint256 amount) public {
    require(msg.sender == owner, "only the owner can decrement");
    require(amount > 0, "amount must be greater than zero");
    require(count >= amount, "counter cannot go below zero");

    count -= amount;

    emit Decrement(msg.sender, amount, count);
}
```

```solidity
function reset() public {
    require(msg.sender == owner, "only the owner can reset");

    count = 0;

    emit Reset(msg.sender);
}
```

📌 Repare na ordem mental correta:

1. valida  
2. muda estado  
3. **conta a história com um event**

---

###  Como isso é usado fora do contrato (visão prática)

Exemplo mental (frontend / script JS):

```javascript
counter.on("Increment", (by, amount, newValue) => {
  console.log(`${by} incrementou ${amount}, novo valor: ${newValue}`);
});
```

Ou buscar histórico:

```javascript
const events = await counter.queryFilter(
  counter.filters.Increment()
);
```

📌 É assim que:

- dashboards  
- UIs  
- indexadores (The Graph)  
- backends Web3  

sabem o que aconteceu, **sem ficar lendo storage a cada bloco**.

---

###  Checkpoint mental - diferenças entre storage e events (guarde isso)

**Storage** = estado atual  
**Event** = histórico do que aconteceu  

Ou ainda:

> contratos **decidem**  
> events **contam a história**

❌ Se você tentar usar `event\` como estado → erro conceitual  
❌ Se você tentar usar `storage\` como log → caro e ruim  

👉 Entender isso separa código funcional de código realmente bem projetado.

---

### 1️⃣ emit pode ser usado para outras coisas?

Resposta curta: **não — e isso é bom.**

---

#### O que `emit` faz exatamente

`emit` **apenas dispara um event**.

Ele:

- **não executa lógica**  
- **não altera estado**  
- **não retorna valor**  
- **não pode falhar sozinho**  

Exemplo:

```solidity
emit Increment(msg.sender, amount, count);
```

É literalmente:

> “registre esse log nos logs da transação”

Nada mais acontece além disso.

---

#### O que NÃO existe (e nunca existiu)

❌ `emit` condicional  
❌ `emit` que influencia fluxo  
❌ `emit` lido por outro contrato  
❌ `emit` como trigger interno  

📌 Se você está pensando em usar `emit` para **controlar comportamento**, você está no caminho errado conceitualmente.

---

#### 📌 recaptulação para "emit" (memorize isso)

> **Se remover todos os `emit` de um contrato,  
> o comportamento onchain dele não muda.**

Isso é **intencional**.

👉 Events existem para **observação**, não para **decisão**.  
👉 `emit` é narrativa, não mecânica.  

Se essa separação estiver clara na sua cabeça,  
você dificilmente vai cometer erros arquiteturais com events.

###  Precisa declarar um event antes de usar `emit`?

✅ **Sim. Sempre. Sem exceção.**

---

#### Como isso funciona em Solidity

Em Solidity:

- `event` define a **assinatura** do log  
- `emit` usa essa definição  

Se o `event` **não existir**:

```solidity
emit SomethingHappened();
```

⛔ **Erro de compilação.**

Não existe:

- “event implícito”  
- “emit solto”  
- “log sem assinatura”  

---

#### Por que isso é obrigatório?

Porque:

- o **nome** do event  
- os **tipos** dos parâmetros  
- quais campos são **indexed**  

Tudo isso compõe o **topic hash** que será gravado nos logs da transação.

📌 A EVM **não aceita logs sem definição prévia**.

Sem essa informação, o log não tem identidade nem possibilidade de indexação.

---

#### Analogia rápida com funções comuns

É como:

- declarar uma função  
- depois chamá-la  

```solidity
event Increment(address indexed by, uint256 amount);
emit Increment(msg.sender, 3);
```

👉 Sem a primeira linha, a segunda **não existe**.

---

#### Regra mental final

> `event` define  
> `emit` executa  

Se você inverter isso na cabeça, o compilador vai te corrigir — com razão.

---

## Tópicos Práticos: (EVM context) Coisas que existem em todo contrato 

Aqui entramos num **checkpoint muito importante**.

Um contrato **não vive isolado**.  
Ele sempre roda dentro de um **contexto de execução fornecido pela EVM**.

Entender isso muda completamente como você lê e escreve contratos.

---

### Principais “variáveis globais” (as mais importantes)

Essas existem **em todo contrato**, sempre disponíveis.

---

#### 🔹 `msg`

Informações da **chamada atual**:

```solidity
msg.sender   // quem chamou
msg.value    // quanto de ETH / MATIC foi enviado
msg.data     // calldata bruta
```

👉 Tudo que depende de **quem chamou** ou **o que foi enviado** vem daqui.

---

#### 🔹 `address(this)`

O endereço do **próprio contrato**.

```solidity
address(this).balance;
```

👉 É assim que você acessa o **saldo do contrato**  
👉 Por isso **não precisamos** de variáveis como `totalDeposited`

📌 O saldo já existe no nível da EVM.

---

#### 🔹 `block`

Informações do **bloco atual**:

```solidity
block.number
block.timestamp
block.chainid
```

⚠️ Importante:

- **não use para aleatoriedade**  
- timestamps podem ser **manipulados levemente por miners / validators**  

👉 Use apenas para regras de tempo **tolerantes**.

---

#### 🔹 `tx`

Contexto da **transação inteira**:

```solidity
tx.origin
```

⚠️ **Quase sempre não deve ser usado**  
(security footgun clássico)

📌 Regra prática:  
Se você acha que precisa de `tx.origin`, provavelmente não precisa.

---

###  Regras especiais sobre `address` e `.balance`

Todo `address`:

- pode ser **EOA** (pessoa)  
- pode ser **contrato**  
- pode **receber ETH**  
- tem `.balance`  

```solidity
address user;
uint256 saldo = user.balance;
```

👉 Não existe “address sem saldo”.

---

### Um contrato recebe ETH se:

- função `receive()` existir  
- ou `fallback()` for `payable`  
- ou alguém usar `selfdestruct`  

Mesmo sem código explícito, ETH **pode chegar**.

---

### Enviar ETH (atualmente se usa call)

Método | Recomendação
--- | ---
`transfer` | ❌ legado
`send` | ❌ legado
`call` | ✅ padrão atual

📌 O *porquê* disso vem depois — o conceito você já tem.

---

###  `public`, `external`, `internal`, `private` (sem confusão)

Essa parte é **fundamental** para escrever contratos limpos.

🧠 Regra mental rápida:

> **Quem pode chamar essa função?**

---

### 🔹 public

Pode ser chamada:

- externamente  
- internamente  

Gera getter automático (para variáveis).

```solidity
function increment() public {}
```

---

### 🔹 external

Só pode ser chamada **de fora**.

- mais eficiente para calldata  
- ideal para funções de interface  

```solidity
function increment() external {}
```

📌 Se você **não chama internamente**, prefira `external`.

---

### 🔹 internal

Só o contrato **e os filhos** (inheritance).

Muito usado para:

- lógica reutilizável  
- modifiers  
- funções auxiliares  

```solidity
function _updateCount() internal {}
```

---

### 🔹 private

Só dentro do **contrato atual**.

Nem contratos filhos acessam.

```solidity
function _secret() private {}
```

---

### Tabela resumo

Visibilidade | Quem pode chamar
--- | ---
public | todos
external | só fora
internal | contrato + filhos
private | só contrato

---

## Como mudar o owner do contrato (padrão real)

Esse é um **padrão real de mercado**.

```solidity
event OwnershipTransferred(
    address indexed oldOwner,
    address indexed newOwner
);

function transferOwnership(address newOwner) public {
    require(msg.sender == owner, "only owner");
    require(newOwner != address(0), "invalid address");

    address oldOwner = owner;
    owner = newOwner;

    emit OwnershipTransferred(oldOwner, newOwner);
}
```

📌 Esse padrão aparece em **quase todos os contratos sérios**.

Depois você vai ver isso encapsulado no:

`Ownable` (OpenZeppelin)

Mas agora você **entende o que ele faz por dentro** — esse é o diferencial.

---

## 🧠 Checkpoint geral (muito importante)

Você agora entende:

- events como **logs offchain**  
- contexto EVM (`msg`, `block`, `address(this)`)  
- por que **não duplicar estado**  
- visibilidade de funções  
- padrão real de ownership  

👉 Isso significa que você **já passou do nível iniciante em Solidity**.

---

## Tópicos Práticos: `Indexed` 

Quando você emite um `event`, a EVM grava um **log**, e esse log é dividido em **duas áreas** bem distintas:

---

### 🔹 Topics (índice)

- dados **indexados**  
- usados para **filtragem**  
- estrutura fixa  
- rápidos de buscar  

---

### 🔹 Data (payload)

- dados **não indexados**  
- servem apenas para **leitura posterior**  
- **não podem** ser filtrados diretamente  

📌 `indexed` decide **em qual dessas áreas** cada parâmetro vai parar.

---

### O que muda quando você marca algo como indexed

```solidity
event Increment(address indexed by, uint256 amount);
```

O que acontece:

- `by` → vai para **topics**  
- `amount` → vai para **data**  

Isso permite consultas como:

```javascript
counter.queryFilter(
  counter.filters.Increment(someAddress)
);
```

👉 Sem `indexed`, **isso não seria possível**.

---

### Limites e regras importantes para indexar

#### ⚠️ Limite duro

- Máximo de **3 parâmetros indexed**  
- O **4º topic** é sempre o **hash do event**  

📌 Esse limite vem da própria EVM.

---

#### ⚠️ Tipos grandes

- Tipos simples (`address`, `uint256`) → armazenados diretamente  
- Tipos complexos (`string`, `bytes`) → **hash** vai para o topic  

📌 Por isso:

- `address indexed` faz sentido  
- `string indexed` quase nunca  

---

### Quando usar indexed

Use `indexed` quando você sabe que alguém vai querer perguntar:

> “Me mostra todos os eventos onde **X** participou”

Casos clássicos:

- `address from`  
- `address to`  
- `owner`  
- `spender`  
- `caller`  

Exemplo padrão (ERC-20):

```solidity
event Transfer(
    address indexed from,
    address indexed to,
    uint256 value
);
```

👉 Esse padrão existe por um motivo muito concreto: **consulta eficiente**.

---

### Quando NÃO usar indexed

❌ Não use para:

- valores agregáveis (`amount`)  
- dados que só fazem sentido juntos  
- coisas que ninguém vai filtrar  

Exemplo ruim:

```solidity
event Updated(uint256 indexed newValue);
```

Porque:

- ninguém filtra por valor exato  
- desperdício de topic  
- perde capacidade de indexar algo realmente útil  

---

###  Custo de gás de indexed

- `indexed` **custa mais gás**  
- mas **não é crítico** na maioria dos casos  

📌 Não micro-otimize isso agora.

👉 **Clareza > micro-otimização**

---

### Regras práticas pra uso de indexed 

🔹 **Indexe quem**  
🔹 **Não indexe quanto**  
🔹 Pense em **consultas futuras**, não no contrato  

Se você imaginar um backend ou UI:

- “quero todos os eventos desse usuário” → `indexed`  
- “quero ver os detalhes” → `data`  

👉 `indexed` é uma decisão de **observabilidade**, não de lógica.

---
## Tópicos Práticos: `modifier` 

Olha para o seu contrato `Counter`.  
Você repetiu várias vezes:

```solidity
require(msg.sender == owner, "only the owner can ...");
```

Isso gera três problemas práticos:

- duplicação de código  
- maior chance de erro (esquecer o `require` em alguma função)  
- leitura mais difícil (a regra importante fica “enterrada” no meio da função)  

👉 `modifiers` existem **exatamente** para declarar essas regras **uma vez** e reaplicá-las.

---

### O que é um modifier (conceitualmente)

Um `modifier` é:

- uma **regra de execução** que envolve uma função  

Ele diz:

> “Antes (e/ou depois) da função rodar, faça isso.”

🧠 Modelo mental correto:

> **modifier = middleware de função**

Nada de mágico. Só composição.

---

### Sintaxe básica (sem mágica)

Exemplo mínimo:

```solidity
modifier onlyOwner() {
    require(msg.sender == owner, "only the owner");
    _;
}
```

O ponto **mais importante** aqui é o `_`.

---

### 🔹 O que é `_`?

- representa o **corpo da função**  
- onde o `_` aparece é onde a função “entra”  

Ou seja, isso:

```solidity
modifier onlyOwner() {
    require(msg.sender == owner);
    _;
}
```

Significa:

1. roda o `require`  
2. executa a função  

📌 Se não existir `_`, a função **nunca roda**.

---

### Usando o modifier na prática

Antes (sem modifier):

```solidity
function increment(uint256 amount) public {
    require(msg.sender == owner, "only owner");
    require(amount > 0);

    count += amount;
}
```

Depois (com modifier):

```solidity
function increment(uint256 amount) public onlyOwner {
    require(amount > 0);
    count += amount;
}
```

💡 Resultado real:

- mais curto  
- mais legível  
- regra de acesso clara no **“título” da função**  

---

### Aplicando em um contrato Counter 

```solidity
pragma solidity ^0.8.20;

contract Counter {
    uint256 public count;
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "only the owner");
        _;
    }

    function increment(uint256 amount) public onlyOwner {
        require(amount > 0, "amount must be greater than zero");
        count += amount;
    }

    function decrement(uint256 amount) public onlyOwner {
        require(amount > 0, "amount must be greater than zero");
        require(count >= amount, "counter underflow");
        count -= amount;
    }

    function reset() public onlyOwner {
        count = 0;
    }
}
```

🔍 Repara como agora:

- a regra de acesso virou parte da **API**  
- a função ficou focada só na **lógica de negócio**  

---

### Modifier pode receber parâmetros? ✅ Sim

Exemplo:

```solidity
modifier minAmount(uint256 min) {
    require(min > 0, "invalid min");
    _;
}
```

Uso:

```solidity
function increment(uint256 amount)
    public
    onlyOwner
    minAmount(amount)
{
    count += amount;
}
```

⚠️ Isso é poderoso, mas use com **parcimônia**.  
Modifiers muito “inteligentes” prejudicam legibilidade.

---

### Modifier pode rodar código depois da função?

✅ Sim. Basta colocar lógica **após** o `_`.

```solidity
modifier logAfter() {
    _;
    // código depois da função
}
```

Casos comuns:

- auditoria  
- eventos pós-execução  
- medidas de segurança  

---

### Boas práticas reais (importante)

✅ Use modifiers para:

- controle de acesso (`onlyOwner`, `onlyAdmin`)  
- estado do contrato (`whenPaused`, `whenNotPaused`)  
- pré-condições reutilizáveis  

❌ Evite usar modifiers para:

- lógica de negócio complexa  
- fluxos difíceis de seguir  
- alterações implícitas demais  

📌 Regra prática:

> **Se o modifier faz mais do que validar contexto, desconfie.**

---

### ligando com o que você já sabe

Você já entendeu:

- `require`  
- `msg.sender`  
- `owner`  
- `events`  

👉 `modifiers` são só:

**regras declarativas reutilizáveis**

Nada de mágico aqui — só organização e segurança.

### Modifiers, require e custom errors — desmistificando o uso correto

#### Contexto da dúvida

Dúvida comum ao evoluir o design de contratos:

> “Eu aprendi a usar modifier com require,  
> mas posso usar modifier com custom errors?  
> E se custom errors são melhores em produção,  
> por que ainda vejo tanto require?”

Essa dúvida é excelente, porque **não é sobre sintaxe**,  
é sobre **design de contrato, ABI e comunicação offchain**.

---

#### Resposta curta (sim)

👉 **Sim, você pode e deve usar modifier com custom errors.**  
👉 **Modifier não é exclusivo de require.**  
👉 Em contratos de produção, o padrão mais sólido hoje é:

- modifier → encapsula regras e invariantes
- if (...) revert CustomError(...) → comunica falhas de forma barata e semântica

---

## Por que isso faz sentido conceitualmente?

Você já captou o ponto central:

- custom errors reduzem bytecode
- viram documentação implícita
- geram dados estruturados para offchain
- são ABI-friendly

Quando combinados com modifiers, cada peça passa a ter **responsabilidade clara**.

---

## 1️⃣ Modifier não é sobre erro

Esse é o primeiro mito a cair.

👉 **Modifier não é sobre lançar erro.**  
👉 Modifier é sobre **expressar uma regra estrutural do contrato**.

Ele comunica algo como:

> “Esta função só pode executar se esta condição estrutural for verdadeira.”

Casos clássicos:

- permissões (owner, role, admin)
- estado do contrato (paused, initialized)
- invariantes globais

📌 *Como* a falha é comunicada não é a função do modifier —  
isso é um detalhe de implementação.

---

## 2️⃣ Custom error é sobre comunicação e custo

Custom error responde a outra pergunta:

> “Se isso falhar, por quê exatamente?”

E aqui ele ganha de require(string) em tudo:

- mais barato em gas
- tipado
- estruturado
- fácil de decodificar offchain
- perfeito para SDKs, UIs e indexadores

📌 **Custom error é linguagem do contrato.**

---

## 3️⃣ Padrão moderno: modifier + custom error

Exemplo simples e correto:


```solidity
error NotOwner(address caller);

modifier onlyOwner() {
if (msg.sender != owner) {
revert NotOwner(msg.sender);
}
_;
}
```

O que existe aqui:

- Regra estrutural clara: onlyOwner
- Erro semântico explícito: NotOwner(address)
- Baixo custo
- Dados úteis para offchain
- Documentação implícita no ABI

Isso já é contrato pensado como interface.

---

## 4️⃣ Comparação direta de padrões

### ❌ Padrão antigo (require + string)

```solidity
modifier onlyOwner() {
require(msg.sender == owner, "Only owner");
_;
}
```

Problemas:

- string é cara
- não é tipada
- não escala
- difícil de tratar offchain de forma confiável
- fraca como documentação de interface

---

### ✅ Padrão moderno (modifier + custom error)

Versão mínima:
```solidity

error OnlyOwner();

modifier onlyOwner() {
if (msg.sender != owner) revert OnlyOwner();
_;
}
```


Versão enriquecida:

```solidity
error Unauthorized(address caller, address expected);

modifier onlyOwner() {
if (msg.sender != owner) {
revert Unauthorized(msg.sender, owner);
}
_;
}
```

📌 Aqui o erro vira parte explícita da API onchain.

---

## 5️⃣ Quando NÃO usar modifier (mesmo com custom errors)

Aqui entra design — vale ser cético.

👉 **Não coloque tudo em modifier só porque é possível.**

Evite modifier quando:

- a regra é específica de uma única função
- a lógica é longa
- a leitura da função ficaria menos clara
- a condição depende fortemente dos parâmetros

Exemplo ruim:

```solidity
modifier validAmount(uint256 amount) {
if (amount == 0) revert InvalidAmount();
_;
}
```

Melhor assim:
```solidity
function deposit(uint256 amount) external {
if (amount == 0) revert InvalidAmount();
...
}
```

📌 Modifiers são para regras transversais,  
não para validação pontual de argumentos.

---

## 6️⃣ Modelo mental recomendado (importante)

Pense assim:

- **Modifier = regra estrutural do contrato**
- **Custom error = linguagem semântica do contrato**

Quando você junta os dois:

- o bytecode fica mais barato
- o ABI vira documentação viva
- o contrato “fala” com o mundo offchain
- integrações ficam mais seguras e previsíveis

Isso já é pensamento de **contrato como produto**, não só código.

---

## 7️⃣ Require não está proibido — só não é o padrão ideal

require ainda faz sentido:

- em protótipos
- em exemplos didáticos
- em checks extremamente simples
- quando erro semântico não importa

Mas em contratos de produção, especialmente públicos:

📌 **Custom errors devem ser a regra, não a exceção.**

---

## 8️⃣ Pergunta de design (para os próximos passos)

Uma checagem importante para evoluir o design:

> Você já está pensando nesses errors como parte da  
> **interface pública do contrato (API onchain)**  
> ou ainda como detalhe interno de implementação?

Essa resposta muda decisões como:

- errors compartilhados
- libs de erros
- versionamento sem quebrar indexadores
- compatibilidade com SDKs

Se isso já está no seu radar, você está no nível certo para avançar.




## Tópicos Práticos : ABI Encoding.

###  O que é ABI Encoding 

ABI Encoding é o **contrato de serialização** entre o mundo EVM e o mundo externo.

Ou, de forma mais explícita:

> É o conjunto de regras que define como dados **tipados**  
> (funções, argumentos, retornos, erros, eventos)  
> são transformados em **bytes** e interpretados de forma idêntica por:
>
> - contratos na EVM  
> - ferramentas off-chain (RPCs, libs, explorers, indexers)

Nada mais. Nada menos.

---

##  A EVM não entende “funções”, “strings” ou “eventos” 

Esse ponto é **crítico** para o modelo mental correto.

A EVM **só entende**:

- bytes  
- posições de memória  
- opcodes  

Logo:

- “chamar uma função”  
- “emitir um evento”  
- “retornar um valor”  
- “lançar um erro”  

👉 tudo isso são **abstrações criadas pelo ABI**, não pela EVM.

O ABI é a linguagem comum entre:

> Solidity ↔ Bytecode ↔ Ferramentas externas

---

### ABI Encoding na ENTRADA do contrato (call data)

Esse é o caso mais conhecido — e você já entende bem — mas vale amarrar.

Quando alguém chama:

```solidity
transfer(address to, uint256 amount)
```

O campo `data` da transação contém:

- [ 4 bytes  ] function selector  
- [ 32 bytes ] `to`  
- [ 32 bytes ] `amount`  

O ABI define:

- como gerar o selector (`keccak256(signature)`)  
- como alinhar tipos em blocos de 32 bytes  
- como lidar com tipos dinâmicos (`string`, `bytes`, arrays)  

📌 Aqui o ABI é usado para **entrar** no contrato.

---

### ABI Encoding na SAÍDA do contrato (return data)

Aqui entra uma parte que muita gente ignora no começo.

Quando uma função retorna:

```solidity
function balanceOf(address user) returns (uint256)
```

Internamente a EVM:

- escreve o valor em memória  
- executa `RETURN(offset, size)`  

⚠️ Mas quem define **o formato desses bytes**?
👉 O ABI.

Exemplo:

```solidity
return 100;
```

É devolvido como:

- [ 32 bytes ] `uint256`  

E fora do contrato:

- `eth_call`  
- `ethers.js`  
- `web3.js`  

sabem exatamente como decodificar isso porque:

> o ABI descreve o layout de saída.

📌 Aqui o ABI é usado para **sair** do contrato.

---

### ABI Encoding em ERROS (revert)

Aqui entra o ponto mais sofisticado do seu estudo atual 👌

---

### ABI Encoding em `require("string")`

```solidity
require(x > 0, "x must be positive");
```

Na prática:

```solidity
revert Error("x must be positive");
```

Encoding:

- [ 4 bytes  ] selector de `Error(string)`  
- [ ...      ] string ABI-encoded  

📌 Esse erro **não faz parte da ABI do contrato**.  
Ele é um padrão **global** da linguagem.

---

###  ABI Encoding em Custom Errors

```solidity
error XMustBePositive(uint256 x);

revert XMustBePositive(x);
```

Encoding:

- [ 4 bytes  ] selector do erro  
- [ 32 bytes ] `x`  

Aqui acontece algo **importante** para o modelo mental:

> **Custom errors SÃO parte da ABI pública do contrato.**

Isso significa que:

- ferramentas externas sabem decodificar  
- auditores conhecem o “vocabulário de falhas”  
- o erro vira parte do design da interface  

📌 Aqui o ABI é usado para **sinalizar falha de forma estruturada**.

---

### ABI Encoding em EVENTS (logs)

Eventos não usam o campo `data` da transação,  
mas usam ABI com **regras próprias**.

```solidity
event Transfer(
    address indexed from,
    address indexed to,
    uint256 amount
);
```

Isso vira:

- `topics[0]` → selector do evento  
- `topics[n]` → parâmetros `indexed`  
- `data` → parâmetros não indexed, ABI-encoded  

Exemplo:

topics:
- [0] `keccak256("Transfer(address,address,uint256)")`  
- [1] `from`  
- [2] `to`  

data:
- [32 bytes] `amount`  

📌 Aqui o ABI é usado para **comunicação assíncrona**, fora do fluxo de execução.

Eventos:

- não podem ser lidos por outros contratos  
- existem exclusivamente para o mundo off-chain  

---

### Um modelo mental unificado (direções, EVM só carrega bytes, ABI da semântica )

Pense assim:

> **ABI Encoding é o formato oficial de mensagem entre contratos e o ecossistema.**

Ele aparece em **4 direções** diferentes:

Direção | Usado para
--- | ---
➡️ Entrada | call data (chamada de função)
⬅️ Saída | return data
❌ Falha | revert + errors
📡 Broadcast | eventos / logs

A EVM só carrega **bytes**.  
O ABI dá **semântica** a esses bytes.

---

### Por que isso importa para escrever e auditar contratos (ABI é design de API)

Você já está no ponto certo para essa pergunta, então vamos ser diretos:

- design de ABI **é design de API**  
- erros fazem parte da interface  
- eventos são contratos com indexadores  
- retornos mal pensados quebram integrações  

📌 ABI mal desenhada = contrato difícil de integrar ou auditar.

Auditoria **não é só**:

> “tem reentrancy?”

É também:

> “essa ABI comunica bem o que o contrato faz  
> e como ele falha?”

---

### Uma provocação (Se você entendeu ABI, consegue contruir tudo apartir apenas dele)

Para testar se o modelo mental fechou mesmo, pense:

> Se eu tivesse que chamar esse contrato **sem Solidity**,  
> apenas com bytes, eu conseguiria?

Se a resposta for:

> “sim, consigo reconstruir tudo a partir da ABI”

👉 então você **realmente entendeu ABI Encoding**.

### ABI Encoding — hashes, 32 bytes e modelo mental correto

#### “Todos os encodings usam selector de 4 bytes e o resto 32? E tudo vem de hashes?”

**Resposta curta:**  
👉 Não.  
Só o *selector* vem de um hash.  
Os valores normalmente **não**.

Agora a resposta correta, com precisão.

---

##### 🔹 1.1 O que é hash de verdade no ABI?

Somente estas coisas vêm de `keccak256`:

| Elemento | Origem |
|--------|--------|
| Function selector (4 bytes) | keccak256("fn(type,...)")[:4] |
| Error selector (4 bytes) | keccak256("ErrorName(type,...)")[:4] |
| Event signature (32 bytes) | keccak256("EventName(type,...)") |

📌 **Somente identificadores vêm de hash.**

---

##### 🔹 1.2 O que **NÃO** vem de hash

Parâmetros como:

- uint256  
- address  
- bool  
- bytes32  

👉 **não são hasheados**  
👉 são valores brutos, apenas **serializados e alinhados em 32 bytes**

Exemplo:

revert XMustBePositive(5);

**Encoding conceitual:**

- [4 bytes ] selector do erro (hash)  
- [32 bytes] 5 ← valor literal, **não hash**

---

#####🔹 1.3 Por que tudo “parece hash”?

Porque:

- tudo é hexadecimal  
- tudo é padding de 32 bytes  
- tudo “parece aleatório” à primeira vista  

Mas conceitualmente:

- **hash = identificação**  
- **ABI encoding = serialização tipada**

---

#### Então por que 32 bytes?

Essa é uma **regra estrutural**, não criptográfica.

A EVM é *word-based*:

- 1 word = 256 bits = **32 bytes**

O ABI escolheu alinhar tudo nisso porque:

- simplifica acesso  
- simplifica decodificação  
- evita layouts ambíguos  

📌 **32 bytes ≠ hash**  
📌 **32 bytes = unidade natural da EVM**

---

### “O encoding é tipo uma tabela nome → valor?”

Excelente pergunta — e a resposta é sutil.

👉 **Não é** uma tabela nome/valor  
👉 É uma **sequência posicional tipada**

❌ **Não existe isso:**

to = 0x123...
amount = 100


✅ **Existe isso:**

posição 0 → address
posição 1 → uint256


O significado vem de **ordem + tipo**, nunca de nomes.

---

### Como pensar no ABI Encoding corretamente

Use este modelo mental:

encode(types[], values[]) → bytes

Exemplo:

types = [address, uint256]
values = [0xabc..., 100]


Resultado:

- [32 bytes address padded]  
- [32 bytes uint256]  

📌 Nenhum nome entra no encoding  
📌 O contrato “sabe” o significado porque ele conhece a **assinatura**

---

### E os tipos dinâmicos? (ABI vira layout de memória)

Aqui o ABI deixa de parecer “tabela” e vira **layout de memória**.

Exemplo:

function foo(string s, uint256 x)

Encoding conceitual:

- [0] offset para string  
- [1] x  
- [2] length da string  
- [3..] bytes da string  

Ou seja:

- o slot **não guarda o valor**  
- guarda **onde o valor começa**

📌 Isso reforça: **ABI é layout, não mapa**

---

### Resumo técnico das regras fundamentais

#### 🔹 Identificação
- Funções → 4 bytes de hash  
- Erros → 4 bytes de hash  
- Eventos → 32 bytes de hash  

#### 🔹 Dados
- Tudo é alinhado em 32 bytes  
- Valores **não são hasheados**  
- Tipos dinâmicos usam **offsets**  
- **Ordem importa, nomes não**

---

### Um teste mental (bom sinal se você conseguir responder)

- Se eu trocar o nome de um parâmetro, o encoding muda?  
  👉 **Não**

- Se eu trocar a ordem dos parâmetros?  
  👉 **Sim, completamente**

- Se eu trocar o tipo uint256 por uint128?  
  👉 **Sim**, mesmo ocupando 32 bytes

Se essas respostas fazem sentido para você, **seu modelo mental está correto**.

### Por que uint256 → uint128 muda o ABI?

#### 1️⃣ A confusão central (normal)

Você pode estar pensando:

> “Mas ambos ocupam 32 bytes… então por que o ABI mudaria?”

Essa intuição é **boa**, mas **incompleta**.

---

### A regra real do ABI (O ABI é definido por tipo + ordem)

👉 **O ABI é definido por tipo + ordem, não por tamanho físico em memória.**

Mesmo que:

- uint128  
- uint256  

ambos sejam serializados em **32 bytes**, eles são **tipos distintos no ABI**.

---

#### Onde isso aparece de forma concreta

##### 🔹 1. Function selector

O selector é gerado a partir da **assinatura textual**:

- add(uint256)  
- add(uint128)  

Essas strings são diferentes →  
keccak256(...) diferente →  
**selector diferente**

📌 **Só isso já muda o ABI.**

---

##### 🔹 2. Decodificação off-chain

Imagine uma ferramenta externa lendo *return data* ou *revert data*.

Ela precisa saber:

- quantos bits aquele número representa  
- como validar  
- como apresentar  

Mesmo que o padding seja o mesmo, o **tipo semântico muda**.

📌 **ABI não é só layout, é contrato semântico.**

---

##### Um exemplo mental forte

Pergunta provocativa:

> Se uint128 e uint256 fossem “iguais”, por que o Solidity não trataria como sinônimos?

Resposta:

👉 Porque o ABI precisa ser **inequívoco**.

O ABI prefere:

- redundância  
- rigidez  
- clareza semântica  

não otimização de bytes.

---

###### Então o que exatamente muda no ABI?

Vamos ser cirúrgicos.

### ❌ O que NÃO muda

- Tamanho do slot (32 bytes)  
- Alinhamento  
- Padding  

### ✅ O que MUDA

- Assinatura da função  
- Function selector  
- ABI JSON (type: uint256 vs uint128)  
- Decodificação por ferramentas externas  
- Compatibilidade com contratos antigos  

📌 **Resultado prático:**  
Um contrato que espera add(uint256) **não reconhece** add(uint128),  
   mesmo que você passe os **mesmos bytes**.

   ---

#####  Onde isso aparece no Hardhat (concreto)

   Isso aparece principalmente nos **artifacts** e nos **testes**.

   ---

#####  Arquivo de artifact

   Após compilar:
   ``` json 
   Dentro dele:

{
    "abi": [ ... ],
    "bytecode": "...",
    "deployedBytecode": "..."
}
```

📌 Esse `abi` é o **ABI oficial do contrato**.

---

##### Comparação real (mental)

Se você trocar:

- add(uint256)

    por:

- add(uint128)

    O ABI muda de:
    ``` json
{
    "name": "add",
        "inputs": [
        { "name": "amount", "type": "uint256" }
        ]
}
``` 
para
``` json

{
    "name": "add",
        "inputs": [
        { "name": "amount", "type": "uint128" }
        ]
}

``` 

Mesmo sem mudar o bytecode de storage.

---

##### Onde isso é usado nos testes

Quando você faz:

await counter.add(5);

O ethers.js:

1. lê o ABI  
2. encontra add(uint256)  
3. gera o selector  
4. faz o ABI encoding  
5. envia a transação  

Se o ABI estiver errado:

- selector errado  
- call falha  
- ou decode errado  

📌 **O ABI governa completamente a interação.**

---

### Importante: ABI ≠ Solidity

Você está fazendo algo **muito saudável** ao separar:

- estudar Solidity  
- estudar ABI como sistema de comunicação  

Muita gente nunca faz isso.

👉 Você está aprendendo o **wire protocol da EVM**.

---

### Gerando call data com ethers (efeito antes da descrição)

#### Visão geral do fluxo

ABI JSON
↓
ethers.Interface
↓
encodeFunctionData(...)
↓
call data (hex)
↓
transação / eth_call



📌 O ABI não é opcional  
📌 O ethers não “adivinha” nada  
📌 Tudo é determinístico

---

#### O ponto exato onde isso acontece

No ethers:
``` js
import {interface} from "ethers"
``` 

O `Interface` é literalmente:

👉 uma implementação do **ABI Encoding/Decoding**

Nada mais.

---

### Exercício mental guiado

Suponha que o ABI tenha:

- add(uint256)

O ethers faz:

1. lê o ABI  
2. encontra "add(uint256)"  
3. gera a assinatura textual  
4. faz keccak256  
5. pega os primeiros 4 bytes  
6. ABI-encode os argumentos  
7. concatena tudo  

📌 Não depende do contrato existir  
📌 Dá pra gerar call data offline

---

#### Gerando call data manualmente

``` js
const abi = [
"function add(uint256 amount)"
];

const iface = new Interface(abi);

const data = iface.encodeFunctionData("add", [5]);

``` 


Resultado conceitual:
``` json
0x
a9059cbb ← selector (4 bytes)
000000...0005 ← uint256(5)
``` 

📌 Isso é o campo `data` da transação  
📌 É exatamente o que vai para a EVM

---

#### O ponto CRÍTICO do modelo mental

Pergunta direta:

> Onde o tipo uint256 foi usado?

Resposta honesta:

- não no valor  
- não no padding  
- **mas na geração do selector**

Se você trocar no ABI para:

- function add(uint128 amount)

O código TS não muda.  
O valor 5 não muda.  
O padding não muda.

👉 **Mas o selector muda.**

---

#### Observação importante

O ethers **não sabe nada** sobre:

- storage  
- lógica  
- bytecode  

Ele só:

- lê ABI  
- gera bytes  
- decodifica bytes  

Por isso:

- ABI errado → call data errado  
- call data errado → contrato “não entende”  

Mesmo que o contrato exista e esteja correto.

---

#### E quando você usa counter.add(5)?

Quando você faz:
``` js
await.counter.add(5)
``` 

O ethers faz **exatamente o mesmo** `encodeFunctionData`.

A única diferença:

- você não vê o hex  
- mas ele existe  

📌 Nada especial acontece  
📌 É só *syntax sugar*

---

### Teste mental final (gerar calldata sem ABI e sem ABI?)

- Se eu tiver só o ABI e nenhum contrato, consigo gerar call data?  
  👉 Sim

- Se eu tiver só o bytecode, sem ABI, consigo chamar funções facilmente?  
  👉 Não

📌 Isso mostra **quem manda na interação**.


---

## Tópicos Práticos: Custom errors

### Contexto da dúvida

Pergunta central:

> “Custom errors são só isso mesmo?  
> É literalmente declarar `error Nome();` e depois dar `revert Nome();`?  
> Não tem mais nada importante que eu deveria saber?”

A intuição está correta — **eles parecem simples demais**.  
E isso costuma acender exatamente a desconfiança certa.

---

#### A sintaxe básica (sem truque escondido)

Sim. No nível mais simples, é exatamente isso:

error XMustBePositive();
``` solidity
if (x <= 0) {
revert XMustBePositive();
}
```

Não existe:

- string
- message
- require
- exceção escondida
- lógica implícita

Você:

1. declara o erro (fora das funções, como structs)
2. reverte chamando o erro

📌 Até aqui: ✔️ é só isso mesmo.

Mas isso é apenas o **caso mínimo**.

---

#### Então por que custom errors existem? (o problema real)

O `require(..., "string")` tem **dois problemas sérios** em contratos reais.

---

##### 🔴Gas e bytecode

Quando você escreve:

require(x > 0, "x must be positive");


O compilador:

- embute a string inteira no bytecode
- gera código para copiar a string para memory
- ABI-encode a string
- retorna isso no revert

➡️ Resultado:

- bytecode maior
- deploy mais caro
- revert caro
- custo pago mesmo que o erro nunca aconteça

Com custom error:

error XMustBePositive();

if (x <= 0) revert XMustBePositive();


No bytecode existe apenas:

- selector do erro (4 bytes)
- nenhum texto
- nenhum dynamic data

➡️ Resultado:

- bytecode menor
- revert MUITO mais barato
- menos ruído em auditoria

---

##### 🔴Semântica fraca com string

Isso aqui:

require(msg.sender == owner, "only owner");


Para a EVM é apenas:

> “reverteu com uma string”

Já isso:

error NotOwner(address caller);

if (msg.sender != owner) {
revert NotOwner(msg.sender);
}


Carrega semântica estrutural:

- erro tem nome
- erro é tipado
- erro pode carregar dados
- erro é decodificável offchain

➡️ Erro vira parte da **API do contrato**, não texto de debug.

---

### Custom errors podem (e devem) ter parâmetros

Eles não são só nomes.

error InsufficientBalance(uint256 available, uint256 required);

if (balance < amount) {
revert InsufficientBalance(balance, amount);
}


Isso permite:

- frontends mostrarem mensagens melhores
- testes validarem exatamente qual erro ocorreu
- SDKs reagirem de forma determinística

⚠️ Mesmo com parâmetros, custom errors ainda são mais baratos que strings.

---

### Onde declarar custom errors (escopo importa)

Você pode declarar errors:

- dentro do contrato
- em interfaces
- em arquivos compartilhados

Exemplo comum:

interface Errors {
error NotOwner();
error ZeroAddress();
}


Uso:

revert Errors.NotOwner();


📌 Isso já é **design de API e padronização**, não só sintaxe.

---

### Require vs revert + custom error

Essas duas formas são equivalentes no controle de fluxo:

require(x > 0);

if (x <= 0) revert();


Mas:

- custom error **só funciona com revert**
- require não aceita custom error

➡️ Isso força:

- validações explícitas
- fluxo mais claro
- separação entre regra e comunicação

Isso é intencional no design da linguagem.

---

### Pegadinhas importantes (herança e nomes)

#### ⚠️ 1. Errors não são herdados magicamente

Declarar um error em um contrato base não o torna automaticamente visível em outros arquivos.

➡️ Organização de código importa.

---

#### ⚠️ 2. O nome do erro importa MUITO

Isso é ruim:

error Error1();


Isso é bom:

error UnauthorizedCaller(address caller);


Porque:

- erro vira linguagem do contrato
- você escreve para humanos + ferramentas
- nome é parte da documentação

---

### ⚠️ 3. Custom error não é exceção “high-level”

Eles:

- não têm stack trace
- não têm mensagem humana embutida
- dependem de decoding offchain

📌 Erro aqui é **protocolo**, não UX.

---

### Quando NÃO usar custom errors

Casos aceitáveis para `require(string)`:

- contratos muito pequenos
- protótipos rápidos
- exemplos didáticos
- código descartável

Em produção, bibliotecas e contratos reutilizáveis:

➡️ custom error quase sempre é a escolha correta.

---

### Gas e bytecode — impacto real (Hardhat comparando uso de gás de dois contratos equivalentes)

Comparando dois contratos equivalentes:

#### Com string

require(x > 0, "x must be positive");


- string embutida no bytecode
- bytecode maior
- deploy mais caro

#### Com custom error

error XMustBePositive();
if (x == 0) revert XMustBePositive();


- só selector bytes4
- bytecode menor
- revert mais barato

📌 Em contratos grandes, isso acumula bastante.

---

### Custom errors fazem parte da ABI pública

Isso é o salto conceitual importante.

Errors aparecem no ABI JSON:

{
"type": "error",
"name": "XMustBePositive",
"inputs": []
}


Isso permite:

- frontends decodificarem `errorName`
- testes esperarem `Error.selector`
- ferramentas integrarem sem heurística

➡️ Error vira **first-class citizen** da interface.

---

### Error como API (analogia útil)

Pense assim:

Camada → Analogia

- Função → endpoint
- Evento → log / output
- Error → HTTP status code

Um bom error é como:

- 401 Unauthorized
- 403 Forbidden
- 409 Conflict

Não como:

- "ops, deu ruim"

---

## Checklist mental rápido 

Sempre que escrever um error, pergunte:

- Esse erro é um limite formal do sistema?
- Um integrador externo deveria reagir a ele?
- Esse nome explica claramente a falha?
- Esse erro vai existir daqui a 1 ano?

Se “sim” para 2 ou mais:
➡️ ele é parte da ABI pública.

---

## Custom errors Conclusão prática

Custom errors:

- não são só sintaxe nova
- não são micro-otimização
- são design de protocolo

Você não está só tratando erro.  
Você está **definindo os limites formais do sistema**.


---

### “Projetar todos os erros antes” — o que isso realmente significa

> Então, na prática, é melhor fazer **toda a projeção de erros** e criar todos os erros **antes** de escrever o código (o que for possível) e só depois escrever o contrato, correto?  
> Evitando o uso de \`require\`, já que são mais caros, além de deixar o contrato mais barato, mais documentado e capaz de alimentar melhor estruturas off-chain?

Resposta curta: **sim, com nuance**.  
Resposta correta: **projetar limites antes, não necessariamente todos os erros imagináveis**.

---


Não é sobre sair listando erros aleatoriamente.  
É sobre **projetar os limites formais do sistema antes do código**.

Erros são a **materialização desses limites**.

---

#### 🔹 O que faz muito sentido projetar antes

Principalmente:

- invariantes
- pré-condições
- barreiras de segurança

Exemplos clássicos:

- \`Unauthorized\`
- \`ZeroAddress\`
- \`InvalidState\`
- \`Paused\`
- \`OverflowNotAllowed\` (quando aplicável)

Esses erros:

- dificilmente mudam
- viram parte da ABI pública
- guiam a implementação

➡️ Aqui, projetar antes **melhora o design**.

---

#### 🔹 O que NÃO faz sentido congelar cedo demais

- regras de negócio ainda instáveis
- protótipos
- contratos descartáveis

Forçar *error-driven design* quando o domínio ainda é nebuloso:

- cria ruído
- gera churn
- vira overengineering

➡️ bom design ≠ rigidez prematura.

---

### “Evitar \`require\` então é sempre melhor?”

Não de forma dogmática.

✔️ Em contratos de produção:
➡️ **sim, na maioria dos casos**

❌ Em:
- testes rápidos
- scripts
- contratos educacionais

\`require\` ainda é ok.

📌 O ponto **não é banir \`require\`**.  
📌 O ponto é **não usar string como API pública**.

---

###  O ganho real de se usar custom errors 

Você entendeu corretamente os ganhos:

✔️ contrato mais barato  
✔️ bytecode menor  
✔️ erro vira sinal semântico off-chain  

Ajuste importante:

“mais documentado” **não** no sentido de comentários,  
mas no sentido de **documentação executável e verificável**.

Isso é muito mais forte.

---

### Aplicando em um Counter mínimo 

#### 📌 Requisitos do sistema (antes do código)

- contador começa em 0
- só o owner pode alterar
- não pode incrementar acima de um limite
- não pode decrementar abaixo de 0

➡️ Esses limites **já são os erros**.

---

#### 🧱 Projeção de erros (primeiro!)

\`error Unauthorized(address caller);\`  
\`error CounterOverflow(uint256 value, uint256 max);\`  
\`error CounterUnderflow(uint256 value);\`

Antes de qualquer função existir,  
o sistema **já está definido**.

---

#### 🧩 Implementação do contrato

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Counter {
    error Unauthorized(address caller);
    error CounterOverflow(uint256 value, uint256 max);
    error CounterUnderflow(uint256 value);

    address public immutable owner;
    uint256 public count;
    uint256 public constant MAX = 10;

    constructor() {
        owner = msg.sender;
    }

    function increment() external {
        if (msg.sender != owner) {
            revert Unauthorized(msg.sender);
        }

        if (count >= MAX) {
            revert CounterOverflow(count, MAX);
        }

        count++;
    }

    function decrement() external {
        if (msg.sender != owner) {
            revert Unauthorized(msg.sender);
        }

        if (count == 0) {
            revert CounterUnderflow(count);
        }

        count--;
    }
}
```

#### O que esse exemplo prova

Esse contrato:

- não usa \`require\`
- não usa strings
- expõe seus limites formais
- é autoexplicativo para humanos **e** máquinas

Quem consome:

- sabe exatamente por que pode falhar
- reage programaticamente
- audita sem contexto externo

➡️ **Error-oriented design funcionando.**

---

#### Insight mais valioso (guarda esse)

Quando você projeta erros **antes** do código:

> o código vira consequência do design,  
> não o contrário.

Isso é um padrão mental poderoso para:

- contratos
- protocolos
- auditoria

---

#### Ordem dos próximos passos (faz sentido)

A ordem que você sugeriu é excelente:

1️⃣ consolidar bem esse modelo  
2️⃣ reforçar com exemplos pequenos  
3️⃣ depois entrar em versionamento / breaking changes  

Porque:

- breaking change só existe quando há API
- errors fazem parte da API

➡️ **A progressão está correta.**

---

### Versionamento e breaking changes (entrada)

Erros **quebram compatibilidade**.

Mudar:

- nome
- assinatura
- parâmetros

➡️ muda selector  
➡️ quebra integradores  
➡️ quebra testes  
➡️ quebra promessas  

Por isso:

> **errors são promessas públicas.**

Quebrar error = quebrar promessa.

---

#### Caminho que vamos seguir a partir daqui

Entramos agora em:

- breaking change real em Solidity
- versionamento de errors
- estratégias compatíveis vs honestamente incompatíveis
- como testar isso tecnicamente no Hardhat

Isso agora faz sentido **porque a base está sólida**.

Seguimos pelo caminho técnico primeiro —  
e depois subimos para design com muito mais clareza.


### Versionamento de Errors e Breaking Changes em Solidity

Perfeito. Então agora a gente entra na parte que quase ninguém trata com seriedade —  
e que, para quem escreve contratos do zero ou audita, é uma das mais importantes.

Vou estruturar assim (bem direto e progressivo):

- O que é breaking change de verdade em Solidity  
- Por que errors quebram compatibilidade  
- Exemplos concretos (bons e ruins)  
- Regras práticas para versionar errors  
- Como um auditor enxerga isso  

---

### O que é breaking change em contratos 

Em web tradicional, você “deploya de novo”.  
Em contratos:

- o código é imutável  
- consumidores existem fora do seu controle  

Então breaking change **não é**:

- “compila”
- “passa nos testes”
- “funciona no frontend atual”

Breaking change **é**:

- alguém que integrava deixa de conseguir reagir corretamente  

E isso inclui:

- funções  
- eventos  
- errors  

---

### Por que errors quebram compatibilidade

Lembra disso?

\`error Unauthorized(address caller);\`

Isso gera:

- nome  
- tipos  
- ordem  
- selector (bytes4)  

Qualquer mudança aqui **muda o selector**.

### 🔴 Mudanças que quebram ABI

`error Unauthorized();`  
→ **QUEBRA** (assinatura mudou)

`error NotAuthorized(address caller);`  
→ **QUEBRA** (nome mudou)

`error Unauthorized(address caller, uint256 time);`  
→ **QUEBRA** (parâmetros mudaram)

Mesmo que:

- o contrato “funcione”
- a regra de negócio seja a mesma  

Para quem integra:  
➡️ **é outro erro**

---

#### Exemplo concreto: Counter v1 → v2 (quebrando tudo)

##### ✅ v1 (bom)

`error CounterOverflow(uint256 value, uint256 max);`

Frontend / bot:

`if (e.errorName === "CounterOverflow") { disableButton(); }`

##### ❌ v2 (ingênuo)

`error MaxValueReached(uint256 current);`

Mesmo significado semântico.  
Mesmo comportamento.  

Mas…

➡️ **100% breaking change**

Tudo que dependia do erro:

- falha  
- cai no catch genérico  
- perde semântica  

---

#### Versão “profissional” de v2 (compatível)

Você tem três estratégias legítimas.

##### 🟢 Estratégia A — Manter o erro antigo

\`error CounterOverflow(uint256 value, uint256 max);\`

Mesmo se internamente você mudou a lógica.

➡️ estabilidade máxima  
➡️ zero breaking change  

---

##### 🟡 Estratégia B — Introduzir novo erro sem remover o antigo

`error counteroverflow(uint256 value, uint256 max);\`  
`error maxvaluereached(uint256 current);\`

e decidir em código qual usar.

➡️ backward-compatible  
➡️ mais complexo  
➡️ exige documentação  

---

##### 🔴 estratégia c — quebrar explicitamente (major version)

- novo contrato  
- novo endereço  
- abi nova  
- users migram conscientemente  

➡️ isso é honesto  
➡️ isso é aceitável  
➡️ isso é raro  

---

### regras práticas para versionar errors (guarda isso)

#### ✔️ 1. erros públicos são quase imutáveis

se você publicou:

`error unauthorized(address);`

considere isso **congelado**.

---

#### ✔️ 2. nome importa mais que mensagem

evite:

`error invalid();`

prefira:

`error unauthorized();`  
`error invalidstate();`  
`error zeroaddress();`

eles sobrevivem melhor ao tempo.

---

#### ✔️ 3. parâmetros também fazem parte do contrato

não adicione parâmetros “porque agora parece útil”.

isso:

`error unauthorized(address caller);`

não pode virar:

`error unauthorized(address caller, uint256 time);`

sem quebrar.

---

#### ✔️ 4. agrupe errors como api

boa prática:

`library errors {  
    error unauthorized(address caller);  
    error invalidstate();  
}`

➡️ deixa explícito que aquilo é “interface”

---

#### como um auditor enxerga isso

quando um auditor vê:

- errors bem nomeados  
- poucos  
- estáveis  
- coerentes  

ele pensa:

> “esse contrato foi projetado, não improvisado”

quando vê:

- strings soltas  
- errors mudando sem razão  
- erros genéricos  

ele pensa:

> “isso vai quebrar integração”

isso **pesa em relatório**.

---

#### o insight final (muito importante)

erros são promessas.

quando você expõe um error:

- você promete que aquela condição existirá  
- você promete que integradores podem confiar nisso  

quebrar error ≈ **quebrar promessa**.

---

### Próximo passo natural 

agora faz muito sentido avançar para:

- como testar compatibilidade de errors no hardhat  
- ou como planejar v2 sem quebrar v1  
- ou como documentar errors como parte do protocolo  

👉 próxima decisão técnica:

seguir em **hardhat + testes + selectors**  
ou subir um nível e discutir **design e versionamento de protocolos**.

ambos fazem sentido — a escolha define onde você quer investir energia agora.


### Testando, protegendo e versionando custom errors no hardhat (nível metal)

perfeito. então vamos descer até o metal, mas sempre com o radar ligado para **por que isso importa** — não só como fazer.

vou organizar em blocos curtos e objetivos:

- como testar custom errors no hardhat  
- como garantir que selectors não mudaram  
- como detectar breaking change automaticamente  
- um micro-workflow técnico saudável  
- o que você passa a “ver” depois disso  


assumindo:

- hardhat  
- ethers  
- mocha / chai  

#### Exemplo com o counter

```ts
import { expect } from "chai";
import { ethers } from "hardhat";

describe("counter", () => {
  it("reverts with counteroverflow", async () => {
    const [owner] = await ethers.getsigners();
    const counter = await ethers.getcontractfactory("counter");
    const counter = await counter.deploy();

    // chega no limite
    for (let i = 0; i < 10; i++) {
      await counter.increment();
    }

    await expect(counter.increment())
      .to.be.revertedwithcustomerror(counter, "counteroverflow");
  });
});
```

🔎 isso testa:

- nome do error  
- abi  
- selector  

sem string. sem heurística.

---

#### Testando parâmetros do error

```ts
await expect(counter.increment())
  .to.be.revertedwithcustomerror(counter, "counteroverflow")
  .withargs(10, 10);
```

➡️ se mudar a **ordem**, **tipo** ou **quantidade** de parâmetros:  
o teste quebra imediatamente.

isso é **ouro para versionamento**.

---

#### Validando selectors explicitamente (nível auditor)

todo error tem um selector:

`bytes4(keccak256("counteroverflow(uint256,uint256)"))`

no hardhat:

```ts
const iface = counter.interface;

const selector = iface.geterror("counteroverflow").selector;

expect(selector).to.equal("0x...");
```

você pode:

- salvar selectors esperados  
- detectar mudanças silenciosas  

---

#### Detectando breaking change automaticamente

aqui está um padrão **muito poderoso**.

### 📌 snapshot de abi

no ci:

- compile  
- salve abi antiga  
- compare com abi nova  

se:

- error sumiu  
- error mudou assinatura  
- error mudou nome  

➡️ **falha o pipeline**

mesmo sem olhar código.

### exemplo simples de comparação (conceitual)

```ts
const olderrors = extracterrors(oldabi);
const newerrors = extracterrors(newabi);

expect(newerrors).to.deep.equal(olderrors);
```

isso trata error como **contrato público**, não detalhe interno.

---

#### Micro-workflow técnico saudável (curto e prático)

quando você cria um contrato novo:

1️⃣ liste os errors  
2️⃣ escreva testes **só de revert**  
3️⃣ implemente a lógica  
4️⃣ rode gas reporter  
5️⃣ congele a abi pública  

quando você muda algo:

- error mudou?  
  → **versiona**  

- não mudou?  
  → **safe**  

---

#### O que muda na sua cabeça depois disso

depois que você começa a:

- testar errors  
- comparar selectors  
- versionar abi  

você para de pensar:

> “o contrato funciona?”

e passa a pensar:

> “o contrato é estável?”

isso é **mentalidade de protocolo**.

---

####  Um detalhe que pouca gente usa (você pode criar um teste **só para abi**)

```ts
it("abi compatibility", async () => {
  const abi = require("../artifacts/contracts/counter.sol/counter.json").abi;

  const errors = abi.filter((x: any) => x.type === "error");

  expect(errors).to.deep.equal([
    {
      type: "error",
      name: "unauthorized",
      inputs: [{ type: "address", name: "caller" }]
    },
    {
      type: "error",
      name: "counteroverflow",
      inputs: [
        { type: "uint256", name: "value" },
        { type: "uint256", name: "max" }
      ]
    },
    {
      type: "error",
      name: "counterunderflow",
      inputs: [{ type: "uint256", name: "value" }]
    }
  ]);
});
```

➡️ isso é **contrato congelado em teste**.

---

### Próximo passo (quais erros são públicos e quais são internos, como evoluir o protocolo)

agora que:

- você sabe testar  
- sabe detectar breaking change  
- sabe proteger a abi  

o próximo passo natural é:

➡️ como decidir quais errors são **públicos** e quais são **internos**  
➡️ como evoluir o protocolo **sem quebrar consumidores**  
➡️ quando **quebrar é aceitável**  

a partir daqui, design deixa de ser abstrato —  
ele passa a ser **ancorado em garantias técnicas reais**.




---
# transição web2 → web3 — fundamentos e arquitetura mental

## 🧠 camada 1 — mudar o modelo mental (fundamental)

### transição web2 → web3: 📦 o que realmente é um smart contract

- um smart contract **não é um backend**
- ele é:
  - um programa determinístico
  - rodando em milhares de máquinas
  - com custo por instrução (gas)
  - sem acesso externo
  - sem io
  - sem relógio confiável
  - sem threads
  - sem exceptions no sentido tradicional

**analogia correta:**
- uma *stored procedure*:
  - distribuída
  - imutável
  - pública
  - paga por uso
  - irreversível
### transição web2 → web3: 🔴 diferença central entre web2 e web3

**web2**
- código pode mudar
- bugs são corrigíveis
- banco de dados é mutável
- acesso é controlado por uma entidade

**web3**
- contratos não podem mudar (na prática)
- bugs custam dinheiro real
- estado é público e imutável
- depois do deploy, ninguém “manda”

👉 isso muda completamente:
- arquitetura
- estratégia de testes
- responsabilidade
- necessidade de paranoia saudável

---


## testes, selectors e proteção de abi com custom errors (hardhat)

### exemplo de teste com custom error

\```ts
import { expect } from "chai";
import { ethers } from "hardhat";

describe("counter", () => {
  it("reverts with counteroverflow", async () => {
    const [owner] = await ethers.getsigners();
    const counter = await ethers.getcontractfactory("counter");
    const counter = await counter.deploy();

    // chega no limite
    for (let i = 0; i < 10; i++) {
      await counter.increment();
    }

    await expect(counter.increment())
      .to.be.revertedwithcustomerror(counter, "counteroverflow");
  });
});
\```

🔎 isso testa:

- nome do error  
- abi  
- selector  

sem string. sem heurística.

---

### testando parâmetros do error

\```ts
await expect(counter.increment())
  .to.be.revertedwithcustomerror(counter, "counteroverflow")
  .withargs(10, 10);
\```

➡️ se mudar a **ordem**, **tipo** ou **quantidade** de parâmetros:  
o teste quebra imediatamente.

isso é **ouro para versionamento**.

---

## 2️⃣ validando selectors explicitamente (nível auditor)

todo error tem um selector:

\`bytes4(keccak256("counteroverflow(uint256,uint256)"))\`

no hardhat:

\```ts
const iface = counter.interface;

const selector = iface.geterror("counteroverflow").selector;

expect(selector).to.equal("0x...");
\```

você pode:

- salvar selectors esperados  
- detectar mudanças silenciosas  

---

## 3️⃣ detectando breaking change automaticamente

aqui está um padrão muito poderoso.

### 📌 snapshot de abi

no ci:

- compile  
- salve a abi antiga  
- compare com a abi nova  

se:

- error sumiu  
- error mudou assinatura  
- error mudou nome  

➡️ **falha o pipeline**, mesmo sem olhar código.

### exemplo simples de comparação (conceitual)

\```ts
const olderrors = extracterrors(oldabi);
const newerrors = extracterrors(newabi);

expect(newerrors).to.deep.equal(olderrors);
\```

isso trata error como **contrato público**, não como detalhe interno.

---

## 4️⃣ workflow técnico saudável (curto e prático)

quando você cria um contrato novo:

1️⃣ liste os errors  
2️⃣ escreva testes **só de revert**  
3️⃣ implemente a lógica  
4️⃣ rode o gas reporter  
5️⃣ congele a abi pública  

quando você muda algo:

- error mudou?  
  → **versiona**  

- não mudou?  
  → **safe**  

---

## 5️⃣ o que muda na sua cabeça depois disso

depois que você começa a:

- testar errors  
- comparar selectors  
- versionar abi  

você para de pensar:

> “o contrato funciona?”

e passa a pensar:

> “o contrato é estável?”

isso é **mentalidade de protocolo**.

---

## 6️⃣ um detalhe que pouca gente usa (mas vale muito)

você pode criar um teste **exclusivo para abi**:

\```ts
it("abi compatibility", async () => {
  const abi = require("../artifacts/contracts/counter.sol/counter.json").abi;

  const errors = abi.filter((x: any) => x.type === "error");

  expect(errors).to.deep.equal([
    {
      type: "error",
      name: "unauthorized",
      inputs: [{ type: "address", name: "caller" }]
    },
    {
      type: "error",
      name: "counteroverflow",
      inputs: [
        { type: "uint256", name: "value" },
        { type: "uint256", name: "max" }
      ]
    },
    {
      type: "error",
      name: "counterunderflow",
      inputs: [{ type: "uint256", name: "value" }]
    }
  ]);
});
\```

➡️ isso é **contrato congelado em teste**.

---

## 7️⃣ próximo passo (agora sim design faz sentido)

agora que:

- você sabe testar  
- sabe detectar breaking change  
- sabe proteger a abi  

o próximo passo natural é:

➡️ decidir quais errors são **públicos** e quais são **internos**  
➡️ aprender a evoluir o protocolo **sem quebrar consumidores**  
➡️ entender **quando quebrar é aceitável**

a partir daqui, design deixa de ser abstrato  
e passa a ser **ancorado em garantias técnicas reais**.
````














## transição web2 → web3: 🧩 camada 2 — base técnica mínima (para não ficar boiando)

aqui o objetivo não é virar especialista, mas ganhar **vocabulário operacional**.

---

### transição web2 → web3: ⚙️ 1️⃣ evm de verdade

estudar:
- o que é a evm
- stack machine
- gas
- storage vs memory vs calldata
- opcodes (conceito, não decorar)

você precisa entender por que:
- loops são perigosos
- arrays grandes são caros
- leitura e escrita têm custos diferentes

👉 isso evita escrever contratos ruins sem perceber.

---

### transição web2 → web3: 🧑‍💻 2️⃣ solidity como linguagem restrita

solidity **não é javascript**.

é uma linguagem:
- com tipagem forte
- focada em estado persistente
- com semântica própria de memória
- cheia de riscos específicos

conceitos essenciais:
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

### transição web2 → web3: 📜 3️⃣ ercs como protocolos sociais

ercs **não são bibliotecas**.
são acordos sociais codificados.

estudar:
- erc-20
- erc-721
- allowance model
- snapshots

entender:
- por que eles existem
- quais ataques exploraram implementações ruins
- como pequenos desvios do padrão causam perdas reais

---

## transição web2 → web3: 🛠️ camada 3 — toolchain (onde tudo começa a fazer sentido)

aqui a maioria se perde — organização é crucial.

---

### transição web2 → web3: 🧪 hardhat (ou foundry)

é o seu:
- ambiente local
- test runner
- deployer
- debugger

você vai:
- rodar blockchain local
- simular ataques
- fazer fork da mainnet
- escrever testes antes do deploy

👉 em web3, quem não testa, **perde dinheiro**.

---

### transição web2 → web3: 🔌 ethers.js

é:
- a ponte entre frontend e contratos
- base de scripts de deploy
- usada em automações off-chain

você precisa entender:
- como instanciar contratos
- como chamar funções
- diferença entre:
  - `call`
  - `sendtransaction`

---

### transição web2 → web3: 🌐 rpc + nodes (na prática)

você **não fala com a blockchain**.
você fala com um **node via rpc**.

infura / alchemy:
- abstraem infraestrutura pesada
- são pontos de confiança

você precisa saber:
- quando confiar
- quando rodar node próprio
- quando usar múltiplos providers

---

## transição web2 → web3: 🏗️ camada 4 — arquitetura de projetos reais

aqui está o objetivo final.

---

### transição web2 → web3: 🧱 padrões de arquitetura on-chain

- factory contracts
- escrow por projeto
- governor + timelock
- multisig admin
- upgradeability vs imutabilidade

aqui entram decisões:
- técnicas
- sociais
- éticas

**exemplo:**
- permitir upgrade → menos risco técnico
- não permitir upgrade → mais confiança social

---

### transição web2 → web3: 🧠 governança ≠ crud

governança envolve:
- poder
- incentivos
- ataques econômicos

você precisa entender:
- quorum
- snapshot
- time delay
- stake vs vote

e principalmente:
- como pessoas abusam do sistema
- mesmo quando o código está “correto”

---

### transição web2 → web3: 🔍 off-chain sem trair o on-chain

serviços off-chain:
- leem
- indexam
- exibem
- notificam

eles **não decidem nada crítico**.

👉 decisão financeira **sempre on-chain**.

---
# 📚 como estudar isso de forma eficaz (método, não links):
## fase 1 — fundamentos práticos

### ler docs ethereum + polygon

## 🧭 guia de estudos — base técnica web3 (ethereum + polygon)

> objetivo:
> construir base técnica sólida para compreender e desenvolver projetos web3
> (smart contracts, arquitetura on-chain/off-chain, governança e segurança),
> partindo do zero prático até um mini-projeto com padrões da indústria.

---
# conceitual

## 🔴 bloco 1 — fundamentos de blockchain & ethereum (obrigatório)

### conceitos gerais
- [x] o que é uma blockchain (revisão técnica)
- [x] diferença entre web2 e web3 (modelo mental)
- [x] imutabilidade e consenso
- [x] estado global da blockchain

### contas e transações
- [x] eoa (externally owned accounts)
- [x] contract accounts
- [x] transações:
  - [x] nonce
  - [x] gas
  - [x] gas limit
  - [x] gas price / base fee
- [x] o que acontece quando uma transação é enviada

🎯 objetivo do bloco:
> conseguir explicar, passo a passo, o que acontece quando alguém chama uma função
> de um contrato na blockchain.

## chamada de funções em smart contracts (fluxo completo)

### visão geral
quando alguém “chama uma função” de um smart contract no ethereum, na prática essa pessoa está **enviando uma transação para o endereço do contrato**, contendo no campo `data` a chamada codificada da função.  
o contrato **não reage automaticamente** a essa chamada; seu código só é executado quando a transação é incluída e executada dentro de um bloco.

---

### passo a passo detalhado (fluxo técnico)

1. **preparação off-chain**
   o usuário interage com uma interface off-chain (wallet, dapp, script, etc.).  
   a função do contrato e seus parâmetros são codificados usando **abi encoding** e colocados no campo `data` da transação.

2. **criação da transação**
   a transação contém, entre outros campos:
   - `from`: endereço eoa do usuário
   - `to`: endereço do smart contract
   - `value`: eth enviado (opcional)
   - `data`: chamada da função codificada
   - `nonce`, `gaslimit`, `maxfeepergas`, etc.

3. **assinatura**
   a transação é:
   - codificada (rlp)
   - hashada
   - assinada com a chave privada do emissor  
   o resultado é a **raw transaction** (bytes representados em hexadecimal).

4. **envio ao nó rpc**
   a raw transaction é enviada via json-rpc (`eth_sendrawtransaction`) a um nó ethereum.  
   o nó verifica:
   - assinatura
   - nonce
   - saldo suficiente para gas e value  
   nenhum código de contrato é executado aqui.

5. **mempool**
   a transação válida entra no mempool.  
   neste estágio:
   - o estado da blockchain não muda
   - o contrato não é executado
   - a transação está apenas aguardando inclusão em um bloco

6. **seleção pelo validador**
   um validador escolhe transações do mempool (geralmente priorizando taxas mais altas) para montar um novo bloco.

7. **execução da transação**
   durante a proposição do bloco, o validador:
   - executa a transação na evm
   - chama o código do contrato indicado em `to`
   - executa a função especificada em `data`
   - consome gas
   - lê e escreve no storage do contrato
   - gera logs e eventos  
   aqui o contrato “existe” e seu código é efetivamente executado.

8. **resultado da execução**
   - se a execução termina com sucesso: o estado global é atualizado.
   - se ocorre `revert` ou falta de gas: o estado é revertido, mas o gas é consumido.

9. **propagação e verificação**
   o bloco é propagado para a rede.  
   todos os outros nós:
   - reexecutam as transações
   - verificam se o estado final e o consumo de gas são válidos  
   se tudo bater, o bloco é aceito.

---

### resposta curta (modelo mental)

quando alguém chama uma função de um smart contract, na verdade está enviando uma transação para o endereço do contrato, contendo a chamada da função no campo `data`.  
essa transação é assinada off-chain, enviada a um nó rpc e colocada no mempool.  
o código do contrato **só é executado quando um validador inclui essa transação em um bloco e a executa na evm**.  
depois disso, todos os nós reexecutam a transação para verificar que o novo estado da blockchain é válido.
---

## 🔴 bloco 2 — smart contracts (modelo mental correto)

- [x] o que é um smart contract (tecnicamente)
- [x] diferença entre:
  - [x] call (leitura)
  - [x] transaction (escrita)
- [x] determinismo
- [x] por que contratos não:
  - [x] acessam internet
  - [x] acessam arquivos
  - [x] acessam tempo real confiável
- [x] como contratos chamam outros contratos
- [x] eventos (logs) e seu papel

🎯 objetivo do bloco:
> entender **limitações e garantias**, não apenas possibilidades.

---

## 🔴 bloco 3 — evm (ethereum virtual machine)

### funcionamento interno (nível correto)
- [x] o que é a evm
- [x] máquina baseada em stack (conceito)
- [x] execução determinística
- [x] gas como custo computacional

### memória e armazenamento
- [x] `storage` (persistente)
- [x] `memory` (temporário)
- [x] `calldata` (somente leitura)
- [x] diferença de custo entre leitura e escrita

### armadilhas comuns
- [x] por que loops são perigosos
- [x] por que arrays grandes custam caro
- [x] o que significa “bricking” um contrato

🎯 objetivo do bloco:
> não escrever código ineficiente ou perigoso sem perceber.

---
# conceitual/>

# pratico>
## 🔴 bloco 4 — solidity (essencial antes de codar)

### base da linguagem
- [ ] tipos básicos
- [x] funções
- [x] construtor
- [x] visibilidade:
  - [x] public
  - [x] external
  - [x] internal
  - [x] private

### contexto de execução
- [x] `msg.sender`
- [ ] `msg.value`
- [ ] `address(this)`
- [ ] `block.number` (conceito, cuidado)

### controle e segurança básica
- [x] `require`
- [ ] `revert`
- [ ] `error`
- [ ] modifiers
- [x] events

🚫 fora de escopo por enquanto:
- inline assembly
- yul
- abi encoding profundo
- otimizações avançadas

🎯 objetivo do bloco:
> ser capaz de ler e escrever contratos simples com clareza.

---

## 🔴 bloco 5 — tokens & padrões (ercs)

### conceitos
- [ ] o que é um token fungível
- [ ] por que tokens são contratos
- [ ] diferença entre token e moeda nativa

### erc-20
- [ ] o que é o padrão erc-20
- [ ] funções principais:
  - [ ] balanceof
  - [ ] transfer
  - [ ] approve
  - [ ] transferfrom
- [ ] allowance model
- [ ] riscos e armadilhas comuns

🎯 objetivo do bloco:
> entender tokens como **infraestrutura padrão**, não como “moedas”.

---

## 🔴 bloco 6 — polygon (visão geral, sem aprofundar)

- [ ] o que é a polygon
- [ ] polygon pos (sidechain)
- [ ] diferença entre polygon e ethereum
- [ ] taxas (gas)
- [ ] matic / pol
- [ ] bridge (conceito geral)

🚫 ignorar por enquanto:
- zkevm
- cdk
- appchains
- soluções enterprise

🎯 objetivo do bloco:
> saber **onde** você está deployando e **por que** usar polygon.

---

## 🔴 bloco 7 — infraestrutura básica (conceitual)

- [ ] o que é um node
- [ ] o que é rpc
- [ ] o papel de infura / alchemy / quicknode
- [ ] diferença entre rodar node próprio e usar provider
- [ ] o que são serviços off-chain
- [ ] o que eles **podem** e **não podem** fazer

🎯 objetivo do bloco:
> entender a fronteira entre on-chain e off-chain.

---

⚠️ só avançar depois de completar os blocos anteriores.
- escrever contratos simples
- [ ] hardhat / foundry
- [ ] testes de smart contracts
- [ ] primeiro contrato simples
- [ ] deploy em testnet
- [ ] frontend mínimo
- [ ] escrow básico
- [ ] factory contracts
- [ ] governança
- quebrar eles de propósito

- entender erros comuns

### fase 2 — segurança
- [ ] segurança avançada

- estudar hacks reais

- entender por que aconteceram

- simular ataques em testes

### fase 3 — mini-projeto

- escrow simples

- token erc-20

- factory

- frontend mínimo

- deploy em testnet

### fase 4 — refinamento

- melhorar arquitetura

- adicionar governança

- escrever readme técnico

- pensar como auditor
---
# 📚 documentação essencial — como usar sem se perder

## 🔹 1) polygon docs  
https://docs.polygon.technology/

👉 **bom, mas perigoso para iniciantes técnicos**

esse conjunto de docs é:
- extremamente completo
- muito amplo
- escrito para vários perfis:
  - infraestrutura
  - zk
  - defi
  - enterprise

📌 use para:
- entender o ecossistema polygon
- saber o que existe
- diferenciar:
  - polygon pos
  - zkevm
  - cdk
  - bridges

🚫 não use como sequência de aprendizado linear  
esses docs **não foram feitos para isso**.

---

## 🔹 2) ethereum developers docs  
https://ethereum.org/developers/docs/

👉 **esse é o seu “docs raiz”**

- melhor material conceitual-técnico existente hoje
- base real de entendimento do ecossistema

📌 use para:
- entender a evm
- entender contas, transações e gas
- entender smart contracts como sistema

👍 é estruturado, mas:
- não é didático no sentido tradicional
- funciona como **referência profunda**

---

## 🔹 3) solidity documentation  
https://docs.soliditylang.org/en/v0.8.31/

👉 **manual da linguagem, não curso**

📌 use para:
- consultar sintaxe
- entender:
  - tipos
  - visibilidade
  - memória
- confirmar comportamentos específicos

🚫 não tente “aprender solidity” lendo isso do começo ao fim  
vai ser improdutivo e frustrante.

---

## 🔹 4) ethereum development docs (eth-develop)  
https://eth-develop.readthedocs.io/

👉 **subestimado e bom**

apesar de mais antigo:
- é mais direto
- tem menos marketing
- foca mais em engenharia “raiz”

📌 bom para:
- criar base mental inicial
- entender conceitos sem ruído

---

## 🔑 2️⃣ documentações adicionais recomendadas

essas complementam muito bem as oficiais.

---

## 🔑 a) openzeppelin learn  
https://docs.openzeppelin.com/learn/

👉 **isso aqui é ouro**

por quê?
- conecta solidity + segurança + padrões
- explica *por que* as coisas são feitas
- mostra armadilhas reais de produção

📌 se você ler apenas **um material além dos oficiais**, que seja este.

---

## 🔑 b) ethereum yellow paper (opcional, seletivo)

👉 não é para ler inteiro

use para:
- entender o papel formal da evm
- saber que existe uma especificação matemática da rede

📌 serve para consulta pontual, não estudo linear.

---

## 🔑 c) hardhat docs (mais tarde)  
https://hardhat.org/docs

👉 **não agora**

📌 use somente quando:
- você estiver prestes a escrever contratos
- já entender evm + solidity básico

antes disso, vira ruído.

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
## Dúvidas:
- Porque se usa call ao invés de transfer e send hoje em dia?

- Tem como usar mais de um modfier em uma função?
