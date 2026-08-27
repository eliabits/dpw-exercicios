# E3 — Testando Conflito de Merge

## 🔀 Testando conflito de merge

**Evidência:**

[Ver evidência do conflito no GitHub](https://github.com/eliabits/dpw-exercicios/blob/main/evidencias/e3-conflito.md#testando-conflito-merge)

---

## 1. Saída do `git merge` que acusou o conflito

**Comando utilizado:**

```bash
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git merge feat/titulo-b

Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

O Git identificou um **conflito de conteúdo no arquivo `README.md`** e interrompeu o merge para que o conflito fosse resolvido manualmente.

---

## 2. Conteúdo do arquivo durante o conflito

O arquivo apresentava os marcadores de conflito do Git:

```text
<<<<<<< HEAD

# DPW — Exercícios do M0

[svg](https://github.com/eliabits/dpw-exercicios/blob/main/evidencias/e3-conflito.md#dpw--exerc%C3%ADcios-do-m0)

=======

# DPW — Exercícios do M

[svg](https://github.com/eliabits/dpw-exercicios/blob/main/evidencias/e3-conflito.md#dpw--exerc%C3%ADcios-do-m)

>>>>>>> feat/titulo-b
```

### O que os marcadores representam?

* `<<<<<<< HEAD` → versão que estava na branch atual (`main`)
* `=======` → separação entre as duas versões
* `>>>>>>> feat/titulo-b` → versão que veio da branch `feat/titulo-b`

---

## 3. Saída do `git log --graph --oneline --all`

**Comando utilizado:**

```bash
eliab@ELIABS MINGW64 /c/dev/Dpw-exercicios (main)
$ git log --graph --oneline --all

* 6750019 (feat/titulo-b) test: trying a conflict
| * b6c237a (HEAD -> main, feat/titulo-a) test: testing a conflict
|/
* b4cc4b2 docs: update e1-ambiente and e2-arqueologia
* ce6127c chore: Criação do gitignore, gitattributes, .env.example, package.json, pnpm-lock.yaml
* 30ea33b Revise README with exercises and author information
* 7217512 Add project title and description to README
```

Esse gráfico mostra que as branches **`feat/titulo-a`** e **`feat/titulo-b`** possuem alterações diferentes a partir de um ponto em comum.

---

## 4. Link permanente para o commit de merge e para a página `/network`

**Commit de merge:**

> O link permanente para o commit de merge deve ser adicionado após a resolução do conflito e a criação do commit de merge.

**Página `/network`:**

[Visualizar o gráfico de branches e commits no GitHub](https://github.com/eliabits/dpw-exercicios/network)

---

## 5. Por que o Git não conseguiu resolver sozinho?

O Git não conseguiu resolver sozinho porque as duas branches modificaram a mesma parte do arquivo `README.md`.

As alterações eram diferentes entre `main` e `feat/titulo-b`, então o Git não conseguiu identificar automaticamente qual versão deveria continuar.

Por isso, foi necessário que o usuário escolhesse ou combinasse manualmente as alterações antes de finalizar o merge.
