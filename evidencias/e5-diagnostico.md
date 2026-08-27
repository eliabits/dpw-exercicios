# Roteiro de Diagnóstico

## 🔎 Tabela de diagnóstico

| **Passo** | **Comando**                                   | **Se a saída for X**                         | **Então**                                                                         |
| --------: | --------------------------------------------- | -------------------------------------------- | --------------------------------------------------------------------------------- |
|     **1** | `pwd`                                         | O caminho não corresponde à pasta do projeto | Entrar na pasta correta usando `cd caminho-do-projeto`                            |
|     **2** | `ls package.json`                             | Retorna `No such file or directory`          | Não estou na raiz do projeto, procurar a pasta correta                            |
|     **3** | `grep "nome-do-pacote" package.json`          | Não encontra o nome do pacote                | O pacote não está declarado no projeto, instalar com `pnpm add nome-do-pacote`    |
|     **4** | `ls node_modules/nome-do-pacote`              | Retorna `No such file or directory`          | As dependências não estão instaladas, executar `pnpm install`                     |
|     **5** | `node -e "require.resolve('nome-do-pacote')"` | Retorna erro `Cannot find module`            | O Node não consegue localizar o pacote, verificar o nome do pacote e a instalação |

---

# 1. Ambiente funcionando

Primeiro verifiquei que o projeto possuía as dependências instaladas.

**Comando:**

```bash id="m8b7xr"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ ls node_modules
```

**Saída:**

```text id="1n6g5q"
prettier@
```

Depois provoquei a falha removendo a pasta `node_modules`.

**Comando:**

```bash id="g0w4xj"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ rm -rf node_modules
```

Agora o projeto não possui mais as dependências instaladas.

---

# 🧪 Executando o roteiro

## Passo 1 — Verificar a pasta atual

**Comando:**

```bash id="5f3j9a"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ pwd
```

**Saída:**

```text id="v4k1py"
/c/dev/Dpw-exercicios
```

**Resultado:**

Estou dentro da pasta correta do projeto.

---

## Passo 2 — Verificar se existe `package.json`

**Comando:**

```bash id="2c8m6w"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ ls package.json
```

**Saída:**

```text id="7r0q2d"
package.json
```

**Resultado:**

O arquivo `package.json` existe, então estou na raiz de um projeto Node.js.

---

## Passo 3 — Verificar se o pacote está declarado

**Comando:**

```bash id="q3n5ts"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ grep "prettier" package.json
    "prettier": "^3.9.6"
```

**Saída:**

```text id="0j9x7c"
"prettier": "^3.9.6"
```

**Resultado:**

O pacote **Prettier** está declarado no `package.json`.

---

## Passo 4 — Verificar se o pacote existe em `node_modules`

**Comando:**

```bash id="f6d2ka"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ ls node_modules/prettier
ls: cannot access 'node_modules/prettier': No such file or directory
```

**Saída:**

```text id="s8v1me"
ls: cannot access 'node_modules/prettier': No such file or directory
```

**Resultado:**

O pacote está declarado no projeto, mas não está instalado no ambiente.

### ❌ Causa encontrada

A causa do problema foi encontrada: **a pasta `node_modules` foi apagada**.

---

# 🛠️ Correção

Para corrigir o problema, executei o comando `pnpm install`.

**Comando:**

```bash id="x5k3rq"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ pnpm install

✓ Lockfile passes supply-chain policies (verified 5h ago)
Lockfile is up to date, resolution step is skipped
Packages: +1
+
Packages are hard linked from the content-addressable store to the virtual store.
  Content-addressable store is at: C:\Users\eliab\AppData\Local\pnpm\store\v11
  Virtual store is at:             node_modules/.pnpm
Progress: resolved 1, reused 1, downloaded 0, added 1, done

devDependencies:
+ prettier 3.9.6

Done in 1s using pnpm v11.24.0
```

---

## ✅ Verificação após a correção

Depois, verifiquei novamente se o pacote estava disponível.

**Comando:**

```bash id="n4c7pz"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ ls node_modules/prettier
```

**Saída:**

```text id="t2v6hd"
node_modules/prettier@
```

**Resultado:**

O pacote **Prettier voltou a ficar disponível** no projeto, confirmando que a execução do `pnpm install` corrigiu o problema.

---

# 📌 Conclusão

O problema ocorreu porque a pasta `node_modules` havia sido removida. O `package.json` continuava declarando o pacote `prettier`, mas os arquivos das dependências não estavam mais instalados localmente.

A execução do `pnpm install` reinstalou as dependências a partir do `pnpm-lock.yaml`, fazendo com que o pacote `prettier` voltasse a ficar disponível.
