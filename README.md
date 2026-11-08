# Plano de Estudos · Oficial Investigador de Polícia (PC-AC)

Dashboard estático em HTML, CSS e JavaScript puros, sem dependências nem etapa de build. Baseado no Edital nº 001/2026 SEAD/PCAC (banca IDECAN). O plano tem 6 horas de estudo por dia e vai de 08/11/2026 a 17/01/2027, uma semana antes da prova prevista para 24/01/2027. O progresso é salvo no navegador (localStorage).

## Publicar no GitHub e na Vercel

1. Crie um repositório vazio no GitHub.
2. Envie estes arquivos para a raiz do repositório (`git init`, `git add .`, `git commit -m "plano"`, `git remote add origin <url>`, `git push -u origin main`).
3. Na Vercel, clique em "Add New Project" e importe o repositório.
4. Em "Framework Preset" deixe "Other". Não preencha comando de build nem diretório de saída.
5. Clique em "Deploy". O endereço público fica pronto em alguns segundos.

## Ajustes comuns

- Datas do cronograma: constantes `START`, `PLAN_END` e `EXAM` no início do script de `index.html`.
- Conteúdo de cada dia: objetos `UNITS`, `P1UNITS`, `P1ORDER`, `P2B` e `THEMES`.
- Se o IDECAN alterar o cronograma, atualize também a seção "Datas importantes" (função `renderTimeline`) e o objeto `MARCOS`.
