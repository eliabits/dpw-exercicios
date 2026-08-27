
# E4 — Desfazendo Alterações com Git

## 📋 Tabela preenchida

| **#** | **Cenário**                                                                   | **Comando**                              |
| ----: | ----------------------------------------------------------------------------- | ---------------------------------------- |
| **1** | Editei um arquivo e quero descartar a alteração (ainda não fiz `add`)         | `git restore <arquivo>`                  |
| **2** | Fiz `git add` do arquivo errado e quero tirá-lo do stage                      | `git restore --staged <arquivo>`         |
| **3** | A mensagem do último commit está errada (ainda não fiz push)                  | `git commit --amend -m "mensagem certa"` |
| **4** | Quero desfazer o último commit, mas manter as alterações no working directory | `git reset --soft HEAD~1`                |
| **5** | Quero reverter um commit **já enviado** para o remoto                         | `git revert <commit>`                    |

---

# 1. Descartar alteração antes do `add`

### Antes

```bash id="j6v9qk"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status

On branch main
nothing to commit, working tree clean
```

### Depois

```bash id="9n1j4m"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status

On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

**Comando utilizado:**

```bash
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git restore README.md
```

**Objetivo:** descartar uma alteração feita no arquivo antes de realizar o `git add`.

---

# 2. Retirar um arquivo do stage

### Antes

```bash id="0q2h8v"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status

On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md
```

### Depois

```bash id="r8x4k1"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status

On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

**Comando utilizado:**

```bash
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git restore --staged README.md
```

**Objetivo:** retirar o arquivo do stage sem apagar as alterações realizadas nele.

---

# 3. Corrigir a mensagem do último commit

### Antes

```bash id="6zq0sd"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status

On branch main
nothing to commit, working tree clean
```

**Comando utilizado:**

```bash
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git commit --amend -m "mensagem certa"
```

### Depois

```bash id="q7m3pf"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git commit --amend -m "mensagem certa"

[main ba99f52] mensagem certa
 Date: Wed Aug 26 17:45:07 2026 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

O comando `git commit --amend` foi utilizado para corrigir a mensagem do último commit.

---

# 4. Desfazer o último commit mantendo as alterações

### Antes

```bash id="c4t9vz"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status

On branch main
nothing to commit, working tree clean
```

**Comando utilizado:**

```bash
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git reset --soft HEAD~1
```

### Depois

```bash id="h2w5ns"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status

On branch main
nothing to commit, working tree clean
```

O `git reset --soft HEAD~1` volta o ponteiro do último commit, mantendo as alterações no histórico de trabalho.

---

# 5. Reverter um commit já enviado para o remoto

### Antes

```bash id="v3k8qa"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status

On branch main
nothing to commit, working tree clean
```

**Comando utilizado:**

```bash
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git revert
```

### Depois

```text id="x1p6rd"
usage: git revert [--[no-]edit] [-n] [-m <parent-number>] [-s] [-S[<keyid>]] <commit>...
   or: git revert (--continue | --skip | --abort | --quit)

    --quit                end revert or cherry-pick sequence
    --continue            resume revert or cherry-pick sequence
    --abort               cancel revert or cherry-pick sequence
    --skip                skip current commit and continue
    --[no-]cleanup <mode> how to strip spaces and #comments
    -n, --no-commit       don't automatically commit
    --commit              opposite of --no-commit
    -e, --no-edit         edit the commit message
    -s, --signoff         add a Signed-off-by trailer
    -m, --mainline <parent-number>
                          select mainline parent
    --no-commit           don't automatically commit
```

> **Observação:** o comando foi executado sem informar o identificador do commit. Por isso, o Git apresentou a mensagem de uso do comando.

O formato correto seria:

```bash
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git revert <commit>
```

---

# 🔎 Reflog

**Comando utilizado:**

```bash id="p9s2le"
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git reflog -10
```

**Saída:**

```text id="k5d7wu"
ba99f52 (HEAD -> main) HEAD@{0}: reset: moving to HEAD
ba99f52 (HEAD -> main) HEAD@{1}: commit (amend): mensagem certa
16a2861 HEAD@{2}: commit: mensagem errada
503a46e HEAD@{3}: commit (merge): fix: merge conflict fixed
b6c237a (feat/titulo-a) HEAD@{4}: checkout: moving from feat/titulo-b to main
6750019 (feat/titulo-b) HEAD@{5}: commit: test: trying a conflict
b4cc4b2 HEAD@{6}: checkout: moving from main to feat/titulo-b
b6c237a (feat/titulo-a) HEAD@{7}: checkout: moving from feat/titulo-b to main
b4cc4b2 HEAD@{8}: checkout: moving from main to feat/titulo-b
b6c237a (feat/titulo-a) HEAD@{9}: merge feat/titulo-a: Fast-forward
```

---

# 🔗 Link permanente para o commit de revert do caso 5

**Link:**

> Adicionar aqui o link permanente do commit de revert depois que o comando `git revert <commit>` for executado corretamente e o novo commit for criado.

---

# 💡 Por que o caso 5 é diferente do caso 4?

O `git reset` remove o último commit do histórico local, mas pode manter as alterações para serem trabalhadas novamente.

Já o `git revert` cria **um novo commit que desfaz as alterações de um commit anterior**, sendo mais adequado quando o commit já foi enviado para o repositório remoto.

Assim, o `reset` altera o histórico, enquanto o `revert` preserva o histórico existente.
