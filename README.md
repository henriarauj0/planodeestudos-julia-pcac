# Plano de Estudos · Oficial Investigador de Polícia (PC-AC)

Dashboard estático em HTML, CSS e JavaScript puros, sem dependências nem etapa de build. Baseado no Edital nº 001/2026 SEAD/PCAC (banca IDECAN) e na grade do curso "Combo PC AC - Oficial Investigador de Polícia - Pós-Edital" (Direito Simples e Objetivo, Hotmart), levantada em 11/11/2026.

A página tem duas partes principais. O cronograma distribui as aulas do curso em blocos de 1 hora, 5 horas por dia, de segunda a sábado. O edital checklist lista o conteúdo programático, disciplina por disciplina, e informa em qual módulo do curso cada disciplina está. Ao marcar um bloco ou um tópico, uma pistola 2D dispara contra a caixa de seleção. O progresso é salvo no navegador (localStorage).

## Como o cronograma é montado

O cronograma vai de 12/11/2026 a 23/01/2027 (véspera da prova) e é calculado pela função `buildPlan` a partir da lista `TRACKS`.

- Segunda a sexta: 5 blocos de teoria e fixação. Cada trilha (uma disciplina ou parte dela) recebe um crédito diário proporcional à quantidade de blocos que tem; as cinco trilhas com mais crédito viram os blocos do dia. Dentro de cada trilha, as aulas seguem a ordem dos módulos na plataforma.
- Datas de liberação: um bloco só entra em um dia igual ou posterior à data em que a aula fica disponível. As aulas com "Estreia 14/11/2026" usam a constante `E`; as aulas com data no título usam essa data.
- Estatística: no máximo 1 bloco de 1 hora por dia. Os blocos de cálculo (Estatística, Matemática Financeira e Raciocínio Lógico) são no máximo 2 por dia e nunca ficam em horas seguidas.
- Ordem dentro do dia: a mesma do dashboard (Contabilidade, Estatística, TI, Análise de Dados, Arquivologia, Administração, Informática, Português, Raciocínio Lógico, Penal, Acre, Legislação Institucional, Constitucional, Administrativo, Redação).
- Prioridade: as matérias de peso 2 e a redação terminam até 15/01/2027; as de peso 1 terminam até 22/01/2027.
- Sábado: 5 blocos de revisão por questões, escritos à mão no objeto `SAT`, usando os módulos QAP 2.0 e os Exercícios de Fixação. Os sábados 21/11/2026 e 02/01/2027 são ocupados pelos dois simulados do curso (5 horas seguidas). O sábado 23/01/2027 tem 3 blocos leves.

- Viagem: de 09/12/2026 a 22/12/2026 não há estudo (constante `TRIPS`). Esses dias aparecem no cronograma como "Viagem · sem estudo" e não recebem blocos. São 10 dias úteis e 2 sábados a menos, isto é, 50 horas de teoria e 10 horas de questões.
- Blocos de menor prioridade: o curso tem 253 blocos de teoria e, com a viagem, restam 210 horas de segunda a sexta. Quando o total não cabe, os blocos listados em `LOW` saem da fila e só voltam se sobrar hora. O que ficar de fora aparece no quadro "Aulas que não couberam no cronograma", abaixo da semana. Se a viagem for removida de `TRIPS`, tudo volta a caber e a lista `LOW` deixa de ter efeito.

Com a viagem, o cronograma tem 210 blocos de segunda a sexta (209 regulares e 1 de menor prioridade), 35 blocos de sábado e 43 blocos fora do cronograma.

## Limitações conhecidas

- A duração das aulas ainda não liberadas não aparece na plataforma. Os blocos dessas aulas foram agrupados por estimativa e podem passar de 1 hora.
- As 210 horas de segunda a sexta são todas consumidas pela teoria, e ainda assim 43 blocos ficaram de fora. A revisão fica restrita aos sábados; não há folga para atrasos.
- A escolha dos blocos de menor prioridade (`LOW`) é um critério editorial: assuntos fora do núcleo do edital, continuações longas de um mesmo tema e, em Penal, crimes com menor incidência esperada. Convém revisar a lista.
- Os sábados 12/12 e 19/12 foram retirados; as questões previstas para eles foram concentradas em 26/12 e 09/01, e os blocos de questões de Informática, Constitucional e Raciocínio Lógico desses dois sábados foram suprimidos.
- Ficaram fora do cronograma: aulas bônus de matemática básica (módulos 27, 28 e 52), Hardware (módulo 26, aulas 51 a 55), aulas 32 a 36 de Raciocínio Lógico (repetem juros e estatística) e aulas 60 a 65 de Direito Administrativo (concursos públicos).
- Não foi localizada aula para: séries temporais (Estatística) e arts. 209 a 212, 342 e 347 do Código Penal.
- 25/12/2026 e 01/01/2027 estão no cronograma como dias normais. Para retirá-los, inclua as datas na constante `OFF_EXTRA`; os blocos são redistribuídos e o que não couber aparece no quadro de aulas fora do cronograma.
- O cronograma é fixo: blocos não marcados em dias passados são contados como atrasados, mas não são remarcados automaticamente.

## Publicar no GitHub e na Vercel

1. Crie um repositório vazio no GitHub.
2. Envie estes arquivos para a raiz do repositório (`git init`, `git add .`, `git commit -m "plano de estudos"`, `git remote add origin <url>`, `git push -u origin main`).
3. Na Vercel, clique em "Add New Project" e importe o repositório.
4. Em "Framework Preset" deixe "Other". Não preencha comando de build nem diretório de saída.
5. Clique em "Deploy". O endereço público fica pronto em alguns segundos.

## Ajustes comuns

- Início e fim do cronograma: constantes `START` e `LAST_WD`. Horas por dia: `SLOTS`.
- Períodos sem estudo: lista `TRIPS`, com `from`, `to` (datas inclusivas) e `label` (texto exibido no dia). Dias avulsos sem estudo: `OFF_EXTRA`.
- Blocos de menor prioridade: lista `LOW`, com o identificador de cada bloco no formato `TRILHA.posição` (a posição começa em 0 e segue a ordem da trilha em `TRACKS`).
- Aulas de cada trilha: lista `TRACKS`. Cada item é `[módulo, aulas e assunto, minutos de vídeo, data de liberação]`. Acrescentar um item ao final de uma trilha não altera as marcações já salvas; inserir ou remover no meio desloca as marcações daquela trilha.
- Prazo de cada trilha: constantes `P2` e `P1`.
- Sábados: objeto `SAT`, uma entrada por data, com `[disciplina, módulo, o que resolver, horas]`.
- Nomes dos módulos do curso: objeto `MOD`. Texto "No curso" de cada disciplina: objeto `COURSE`.
- Data da prova: constante `EXAM`.
- Tópicos do edital: objeto `TOPICS` (a chave `RED` guarda os temas de redação, que também geram os blocos de redação de treino).
- Disciplinas, pesos e número de questões: objeto `SUBJ`; a ordem de exibição está em `SPEC`, `BASIC` e `ORDER`.
- Frases motivacionais: lista `QUOTES`.
- Animação do tiro: desenho em `GUN_SVG`, função `shoot` e os `@keyframes` `gun`, `flash`, `bullet`, `burst` e `spark` no CSS. Ela é exibida mesmo quando o sistema está com "reduzir movimento" ligado, por ser o efeito central da página.
- Se o IDECAN alterar o cronograma do concurso, atualize a seção "Datas importantes" (função `renderTimeline`).

## Dados salvos

O progresso continua na chave `edital-pcac-oi-v3`; os tópicos já marcados na versão anterior são mantidos. Os blocos do cronograma ficam no campo `blk` dessa mesma chave. O botão "Reiniciar progresso" apaga tópicos, blocos e simulados.
