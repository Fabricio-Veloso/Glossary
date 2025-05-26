# chown

- O comando `chown` (change owner) é usado para alterar o proprietário e/ou o grupo de um arquivo ou diretório no sistema Linux/Unix.

### Sintaxe

```bash
chown [OPÇÕES] NOVO_PROPRIETÁRIO[:NOVO_GRUPO] ARQUIVO/DIRETÓRIO
```

- Se o grupo for omitido, só o proprietário será alterado.

- Pode usar -R para aplicar recursivamente em diretórios.

## Exemplos

- Muda o proprietário do arquivo 'meuarquivo.txt' para o usuário 'fab'

```
chown fab meuarquivo.txt
```

- Muda o proprietário para 'fab' e o grupo para 'dev' no arquivo 'meuarquivo.txt'

```
chown fab:dev meuarquivo.txt
```

- Aplica recursivamente, mudando dono e grupo de todos os arquivos dentro da pasta 'projeto'

```
chown -R fab:dev projeto/
```

---

# chmod

### O comando chmod (change mode) altera permissões de leitura, escrita e execução de arquivos e diretórios.

#### Sintaxe

```
chmod [OPÇÕES] MODO ARQUIVO/DIRETÓRIO
```

- MODO pode ser simbólico (r, w, x) ou numérico (ex.: 755).

- Pode usar -R para aplicar recursivamente em diretórios.

#### Modos numéricos (mais comuns)

- 4 leitura (r)
- 2 escrita (w)
- 1 execução(x)

#### Soma dos valores para definir permissões:

- Dono (user)

- Grupo (group)

- Outros (others)

#### Exemplo: chmod 755 arquivo

- Dono: 7 (4+2+1) = leitura, escrita e execução

- Grupo: 5 (4+0+1) = leitura e execução

- Outros: 5 (4+0+1) = leitura e execução

#### Exemplos

- Dá permissão de execução para o dono do arquivo 'script.sh'

```
chmod u+x script.sh
```

- Remove permissão de escrita para o grupo em 'arquivo.txt'

```
chmod g-w arquivo.txt
```

- Dá permissão total para o dono e leitura/execução para grupo e outros no diretório 'meuapp' (recursivo)

```
chmod -R 755 meuapp/
```

- Permite leitura e escrita para todos (dono, grupo e outros)

```
chmod 666 arquivo.txt
```
