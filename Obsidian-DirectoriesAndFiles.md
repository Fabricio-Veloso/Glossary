## Obter Arquivo Ativo

```ts
const file = app.workspace.getActiveFile();
```

## Caminho do Arquivo Ativo

```
const path = app.workspace.getActiveFile()?.path;
```

Obter Pasta Pai do Arquivo Ativo

```
const parentPath = app.workspace.getActiveFile()?.parent?.path;
```

Listar Arquivos do Vault

```
const files = app.vault.getFiles();
```

Listar Todos os Arquivos e Pastas

```
const all = app.vault.getAllLoadedFiles();
```

Filtrar Apenas Pastas

```
import { TFolder } from 'obsidian';

export function logProgressCb() {
	const folders = app.vault.getAllLoadedFiles().filter(f => f instanceof TFolder);
	console.log(folders);
}
```

Filtrar Arquivos por Extensão

```
const mdFiles = all.filter(f => f instanceof TFile && f.extension === "md");
```

Obter Objeto de Arquivo por Caminho

```
const file = app.vault.getAbstractFileByPath("projetos/x/_b.md");
```

Verificar se Arquivo Existe

```
const existe = !!app.vault.getAbstractFileByPath("caminho.md");
```

Criar Arquivo Markdown

```
await app.vault.create("pasta/arquivo.md", "conteúdo");
```

Criar Pasta

```
await app.vault.createFolder("projetos/novo");
```

Verificar se Pasta Existe

```
const existe = app.vault.getAbstractFileByPath("projetos") instanceof TFolder;
```

Caminho Relativo de um Arquivo

```
const path = file.path;
```

Nome do Arquivo Sem Extensão

```
const nome = file.basename;
```

Caminho Absoluto Completo

```
const fullPath = app.vault.adapter.getFullPath(file.path);
```

Renomear Arquivo

```
await app.vault.rename(file, "novo/nome.md");
```

Mover Arquivo para Outra Pasta

```
await app.fileManager.renameFile(file, "nova-pasta/" + file.name);
```

Apagar Arquivo

```
await app.vault.delete(file);
```

Apagar Pasta

```
await app.vault.deleteFolder(folder);
```

Criar Caminho Condicional

```
const caminho = ["projetos", escopo, projeto, "_b.md"].join("/");
```

Criar Subpastas Condicionalmente

```
if (!(app.vault.getAbstractFileByPath("atividades") instanceof TFolder)) {
  await app.vault.createFolder("atividades");
}
```

Verificar se Caminho é Pasta

```
const abstrato = app.vault.getAbstractFileByPath("algum/ponto");
const ehPasta = abstrato instanceof TFolder;
```
