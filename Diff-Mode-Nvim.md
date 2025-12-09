
# Glossário — Diff Mode no Neovim

## Ativar e Desativar Diff
### Ativar diff manualmente em cada split
```
:diffthis
```

### Desativar diff no split atual
```
:diffoff
```

### Desativar diff em todos os splits do tabpage
```
:diffoff!
```

### Atualizar as diferenças (recalcular)
```
:diffupdate
```

---

## Navegação entre blocos de diferença
### Próximo bloco de diff
```
]c
```

### Bloco de diff anterior
```
[c
```

---

## Copiar diferenças entre buffers
Esses comandos só funcionam totalmente se **ambos os splits estiverem em diff mode no mesmo tabpage**.

### Pegar a mudança do outro buffer (trazer pro atual)
**Keymap padrão:**
```
do
```

**Comando equivalente:**
```
:diffget
```

---

### Enviar a mudança do buffer atual para o outro
**Keymap padrão:**
```
dp
```

**Comando equivalente:**
```
:diffput
```

---

## Abrir arquivos já iniciando diff
### Abrir verticalmente comparando com o buffer atual
```
:vert diffsplit caminho/do/arquivo
```

### Abrir horizontalmente comparando com o atual
```
:diffsplit caminho/do/arquivo
```

---

## Checar estado do diff
### Ver se o split está em diff
```
:set diff?
```

### Ver opções do diff
```
:set diffopt?
```

---

## Observações úteis (curtas)
- `do` = *diff obtain* → pega do outro lado.  
- `dp` = *diff put* → envia para o outro lado.  
- Se `dp` “apaga linha” é porque os splits **não estão no mesmo grupo de diff**.  
- Plugins como Neo-tree/Telescope não quebram diff, mas você deve rodar `:diffthis` depois que o arquivo abrir.

