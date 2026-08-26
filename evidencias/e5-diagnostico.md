## Roteiro de Diagnóstico

| Passo | Comando | Se a saída for X | Então |
|---|---|---|---|
| 1 | `pwd` | O caminho não corresponde à pasta do projeto | Entrar na pasta correta usando `cd caminho-do-projeto` |
| 2 | `ls package.json` | Retorna `No such file or directory` | Não estou na raiz do projeto, procurar a pasta correta |
| 3 | `grep "nome-do-pacote" package.json` | Não encontra o nome do pacote | O pacote não está declarado no projeto, instalar com `pnpm add nome-do-pacote` |
| 4 | `ls node_modules/nome-do-pacote` | Retorna `No such file or directory` | As dependências não estão instaladas, executar `pnpm install` |
| 5 | `node -e "require.resolve('nome-do-pacote')"` | Retorna erro `Cannot find module` | O Node não consegue localizar o pacote, verificar o nome do pacote e a instalação |

1. Ambiente funcionando

Primeiro verifiquei que o projeto possuía as dependências instaladas:
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ ls node_modules
prettier@

 Depois provoquei a falha:

eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ rm -rf node_modules

Agora o projeto não possui mais as dependências instaladas.

**Executando o roteiro**
Passo 1 — Verificar a pasta atual

*Comando:*

eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ pwd

*Saída:*

/c/dev/Dpw-exercicios

Resultado:
Estou dentro da pasta correta do projeto.

Passo 2 — Verificar se existe package.json

Comando:

eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ ls package.json

Saída:

package.json

Resultado:

O arquivo package.json existe, então estou na raiz de um projeto Node.js.

Passo 3 — Verificar se o pacote está declarado

Comando:

eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ grep "prettier" package.json
    "prettier": "^3.9.6"

Saída:

 "prettier": "^3.9.6"

Resultado:

O pacote está declarado no package.json.

Passo 4 — Verificar se o pacote existe em node_modules

Comando:

eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ ls node_modules/prettier
ls: cannot access 'node_modules/prettier': No such file or directory

Saída:

ls: cannot access 'node_modules/prettier': No such file or directory

Resultado:

O pacote está declarado no projeto, mas não está instalado no ambiente.

A causa do problema foi encontrada: a pasta node_modules foi apagada.


##Correção

**Executei:**

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


Depois verifiquei novamente:

eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ ls node_modules/prettier
node_modules/prettier@

O pacote voltou a ficar disponível.