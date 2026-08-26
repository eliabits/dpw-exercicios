## TESTANDO CONFLITO MERGE

**a saída do git merge que acusou o conflito;**
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git merge feat/titulo-b  
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.

**o conteúdo do arquivo durante o conflito, com os marcadores (copie antes de resolver);**
<<<<<<< HEAD
# DPW — Exercícios do M0
=======
# DPW — Exercícios do M

>>>>>>> feat/titulo-b

**a saída de git log --graph --oneline --all;**
6750019 (feat/titulo-b) test: trying a conflict
| * b6c237a (HEAD -> main, feat/titulo-a) test: testing a conflict
|/  
* b4cc4b2 docs: update e1-ambiente and e2-arqueologia
* ce6127c chore: Criação do gitignore, gitattributes, .env.example, package.json, pnpm-lock.yaml
* 30ea33b Revise README with exercises and author information
* 7217512 Add project title and description to README

**link permanente para o commit de merge e para a página …/network;**

**em 3 linhas: por que o Git não conseguiu resolver sozinho?**
o git não resolve sozinho o conflito pois precisa que o usuário dia qual versão é a que vai continuar