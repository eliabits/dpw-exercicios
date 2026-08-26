
**a tabela preenchida;**
| **#** | **Cenário**                                                                   | **Comando**                             |
| ----: | ----------------------------------------------------------------------------- | --------------------------------------- |
|     1 | Editei um arquivo e quero descartar a alteração (ainda não fiz `add`)         | `git restore           |
|     2 | Fiz `git add` do arquivo errado e quero tirá-lo do stage                      | `git restore --staged   |
|     3 | A mensagem do último commit está errada (ainda não fiz push)                  | `git commit --amend -m  |
|     4 | Quero desfazer o último commit, mas manter as alterações no working directory | `git reset --soft  HEAD~1            |
|     5 | Quero reverter um commit **já enviado** para o remoto                         | `git revert        |
---
---

**para cada caso, a saída de git status ou git log --oneline -3 antes e depois;]**
**CASO 1:**
- antes: 
$ git status
On branch main
nothing to commit, working tree clean
- depois: 
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
 
 ---

**CASO 2:**
- antes: 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md


- depois: 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

---

**CASO 3:**
- antes: 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status
On branch main
nothing to commit, working tree clean


- depois: 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git commit --amend -m "mensagem certa"
[main ba99f52] mensagem certa
 Date: Wed Aug 26 17:45:07 2026 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)

---
**CASO 4:**
- antes: 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status
On branch main
nothing to commit, working tree clean

- depois: 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git reset --soft 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status
On branch main
nothing to commit, working tree clean


**CASO 5:**
- antes: 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git status
On branch main
nothing to commit, working tree clean

- depois: 
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git revert
usage: git revert [--[no-]edit] [-n] [-m <parent-number>] [-s] [-S[<keyid>]] <commit>...
   or: git revert (--continue | --skip | --abort | --quit)

    --quit                end revert or cherry-pick sequence
    --continue            resume revert or cherry-pick sequence
    --abort               cancel revert or cherry-pick sequence
    --skip                skip current commit and continue
    --[no-]cleanup <mode> how to strip spaces and #comments from message
    -n, --no-commit       don't automatically commit
    --commit              opposite of --no-commit
    -e, --[no-]edit       edit the commit message
    -s, --[no-]signoff    add a Signed-off-by trailer
    -m, --[no-]mainline <parent-number>
                          select mainline parent
    --[no-]rerere-autoupdate
                          update the index with reused conflict resolution if possible
    --[no-]strategy <strategy>
                          merge strategy
    -X, --[no-]strategy-option <option>
                          option for merge strategy
    -S, --[no-]gpg-sign[=<key-id>]
                          GPG sign commit
    --[no-]reference      use the 'reference' format to refer to commits

---
**a saída de git reflog -10 no final;**
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git reflog -10
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

---
**link permanente para o commit de revert do caso 5;**


---
**em 3 linhas: por que o caso 5 é diferente do 4?**
o comando reset Remove o último commit do histórico local, mas mantém as alterações, o revert cria um novo commit que desfaz as alterações do commit "revertido"