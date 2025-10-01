# GitHub Contribution Grid Snake

---

## 👀 O que é

O projeto coleta o *contribution graph* do GitHub (a grade 7x52) e gera uma animação onde uma cobra percorre e "come" as células conforme o nível de contribuição. O artefato gerado pode ser SVG animado ou GIF, permitindo que você inclua a animação diretamente no seu README de perfil.

---

## ✨ Exemplo (para incluir no seu README de perfil)

```md
<div align="center">
  <img src="https://raw.githubusercontent.com/<SEU_USUARIO>/<REPO>/output/github-contribution-grid-snake.svg" alt="GitHub Contribution Grid Snake" />
</div>
```

Substitua `<SEU_USUARIO>` e `<REPO>` pelos valores corretos (normalmente o repo criado com seu *username* quando quer fazer o README de perfil).

---

## 🧩 Principais recursos

* Gera SVG animado ou GIF a partir do contribution graph.
* Permite customizar cores, intervalo de frames, tamanho e formato de saída.
* Fácil de integrar via GitHub Actions e automatizar a atualização diária.

---

## 🚀 Como usar (forma rápida)

1. Fork deste repositório (ou clone e ajuste como preferir).
2. Crie/edite o workflow em `.github/workflows/main.yml` no seu repositório de README (ou neste repositório) usando a Action que gera a arte.
3. Configure permissões de `Read and write` para que o workflow possa commitar o arquivo de saída (se necessário).
4. Habilite o workflow em **Actions** e rode-o manualmente ou espere a execução agendada.

> Dica: muitos forks usam um branch `output` para commitar apenas o arquivo final (SVG/GIF) e manter o histórico do `main` limpo.

---

## ⚙️ Exemplo de workflow (`.github/workflows/snake.yml`)

Aqui está um exemplo de workflow usando a action conhecida **Platane/snk** (compatível com esta abordagem). Ajuste `with:` conforme suas preferências.

```yaml
name: Generate Contribution Snake

on:
  workflow_dispatch:
  schedule:
    - cron: '0 0 * * *' # roda todo dia à meia-noite UTC

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Generate contribution snake
        uses: Platane/snk@v3.3.0
        with:
          username: ${{ github.repository_owner }}
          format: svg # svg|gif
          output: output/github-contribution-grid-snake.svg
          # colors: '#EBEDF0,#9BE9A8,#40C463,#30A14E,#216E39' # opcional

      - name: Commit & push output
        uses: stefanzweifel/git-auto-commit-action@v4
        with:
          commit_message: Generated contribution snake
          file_pattern: output/*
```

> Esse exemplo usa `Platane/snk@v3.3.0` como gerador — é uma implementação popular para esse propósito (você pode trocar a versão). citeturn2search2

---

## 🔧 Entradas/configurações comuns

* `username`: GitHub username cujo gráfico será usado.
* `format`: `svg` ou `gif`.
* `output`: caminho do arquivo gerado (ex.: `output/github-contribution-grid-snake.svg`).
* `colors`: lista de cores (4–5) que o gerador usa para as intensidades da grade.
* `scale` / `cell-size`: opções de tamanho (dependem da action utilizada).

Consulte a documentação da Action que escolher para ver todas as opções disponíveis. Exemplos e variações podem ser encontrados em repositórios similares e tutoriais online. citeturn2search0turn2search1

---

## 🖼️ Como exibir no README do seu perfil

1. Após o workflow gerar `output/github-contribution-grid-snake.svg`, copie a URL raw (ex.: `https://raw.githubusercontent.com/<SEU_USUARIO>/<REPO>/output/github-contribution-grid-snake.svg`).
2. Cole no README principal com a tag `img` ou markdown `![]()` conforme o exemplo no topo.

---

## 🛠️ Solução de problemas comuns

* **SVG/GIF aparece estranho ao abrir direto no GitHub**: às vezes o GitHub tenta renderizar o arquivo em HTML ou altera a forma como o conteúdo é servido. Usar a URL raw (`raw.githubusercontent.com`) normalmente resolve. Também verifique se o arquivo não está corrompido pelo processo de commit. citeturn2search6

* **Workflow falha por permissão**: configure `Permissions` do workflow para permitir gravação no repositório (Read & Write). Em repositórios de perfil, dê atenção especial às permissões do repositório que contém o README.

---

## 🤝 Contribuindo

Contribuições são bem-vindas!

* Abra uma issue descrevendo a melhoria ou bug.
* Para mudanças rápidas, envie um PR com um branch claro e teste o workflow.

---
