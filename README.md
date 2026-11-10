# Edital Checklist · Oficial Investigador de Polícia (PC-AC)

Dashboard estático em HTML, CSS e JavaScript puros, sem dependências nem etapa de build. Baseado no Edital nº 001/2026 SEAD/PCAC (banca IDECAN). Não há cronograma: o conteúdo programático é apresentado como uma checklist, disciplina por disciplina, e cada tópico é marcado quando concluído. Ao marcar um tópico, uma pistola 2D dispara contra a caixa de seleção. O progresso é salvo no navegador (localStorage).

## Publicar no GitHub e na Vercel

1. Crie um repositório vazio no GitHub.
2. Envie estes arquivos para a raiz do repositório (`git init`, `git add .`, `git commit -m "edital checklist"`, `git remote add origin <url>`, `git push -u origin main`).
3. Na Vercel, clique em "Add New Project" e importe o repositório.
4. Em "Framework Preset" deixe "Other". Não preencha comando de build nem diretório de saída.
5. Clique em "Deploy". O endereço público fica pronto em alguns segundos.

## Ajustes comuns

- Data da prova: constante `EXAM` no início do script de `index.html`.
- Tópicos de cada disciplina: objeto `TOPICS` (a chave `RED` guarda os temas de redação). Acrescentar um tópico ao final de uma lista não altera o progresso já salvo; inserir ou remover no meio desloca as marcações daquela disciplina.
- Disciplinas, pesos e número de questões: objeto `SUBJ`; a ordem de exibição está em `SPEC`, `BASIC` e `ORDER`.
- Frases motivacionais: lista `QUOTES`.
- Animação do tiro: desenho em `GUN_SVG`, função `shoot` e os `@keyframes` `gun`, `flash`, `bullet`, `burst` e `spark` no CSS. Ela é exibida mesmo quando o sistema está com "reduzir movimento" ligado, por ser o efeito central da página.
- Se o IDECAN alterar o cronograma do concurso, atualize a seção "Datas importantes" (função `renderTimeline`).

## Migração da versão com cronograma

O progresso passou a ser salvo na chave `edital-pcac-oi-v3`. Na primeira abertura, o nome, o tema, a meta e os simulados registrados na versão anterior (`plano-pcac-oi-v2-6h`) são aproveitados. As tarefas diárias marcadas na versão antiga não são convertidas, porque não correspondem um a um aos tópicos do edital.
