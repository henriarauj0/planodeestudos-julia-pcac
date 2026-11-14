# Plano de Estudos · Oficial Investigador de Polícia (PC-AC)

Dashboard estático em HTML, CSS e JavaScript puros, sem dependências nem etapa de build. Baseado no Edital nº 001/2026 SEAD/PCAC (banca IDECAN) e na grade do curso "Combo PC AC - Oficial Investigador de Polícia - Pós-Edital" (Direito Simples e Objetivo, Hotmart), levantada em 11/11/2026. Cronograma refeito em 14/11/2026.

A página tem duas partes principais. O cronograma distribui as aulas do curso em 6 horas por dia, de segunda a sexta, com duas matérias por dia. O edital checklist lista o conteúdo programático, disciplina por disciplina, e informa em qual módulo do curso cada disciplina está. Ao marcar um bloco ou um tópico, uma pistola 2D dispara contra a caixa de seleção. O progresso é salvo no navegador (localStorage).

## Como o cronograma é montado

O cronograma vai de 16/11/2026 a 22/01/2027 (sexta-feira antes da prova) e é calculado pela função `buildPlan` a partir das listas `TRACKS` e `GROUPS`.

- Duas matérias por dia, 3 horas cada. Em cada matéria, as duas primeiras horas são de aulas novas e a terceira é de questões do mesmo assunto (módulos QAP 2.0 e Exercícios de Fixação).
- Ordem das aulas: dentro de cada matéria, as aulas seguem a ordem dos módulos na plataforma. Uma aula só entra em um dia igual ou posterior à data em que fica disponível. As aulas com "Estreia 14/11/2026" usam a constante `E`; as aulas com data no título usam essa data.
- Escolha das matérias do dia: cada matéria acumula um crédito diário proporcional ao número de sessões que ainda precisa; as duas com mais crédito viram as matérias do dia. As de peso 2 recebem 20% a mais de crédito, para terminarem antes.
- Matérias de cálculo: Estatística, Matemática financeira e Raciocínio Lógico nunca caem no mesmo dia.
- Peso 2: Contabilidade (com Matemática financeira), Estatística, TI, Análise de Dados, Arquivologia e Administração entram completas e terminam até 14/01/2027.
- Peso 1: só entram as aulas listadas em `FOCUS`. Português, Informática, Raciocínio Lógico e Processo Penal têm de três a quatro sessões cada. Realidade do Acre, Legislação Institucional, Constitucional e Administrativo têm uma ou duas sessões cada, porque o item 10.5 do edital elimina quem zerar qualquer disciplina.
- Redação: quatro blocos de aula e seis redações de treino, em cinco sessões; a terceira hora de cada sessão é de correção pelos critérios do edital.
- Viagem: de 09/12/2026 a 22/12/2026 não há estudo (constante `TRIPS`). Nas duas semanas seguintes, a primeira hora de questões de cada matéria já iniciada é de revisão do que foi visto antes da viagem.
- Dias fixos (objeto `FIXED`): 15/01/2027 tem o Simulado 02 do curso (5 horas) e 1 hora de correção; 22/01/2027 é de revisão final.
- Se sobrar sessão, entram os blocos de `LOW` e, depois, sessões de revisão por questões.

Com a viagem, são 40 dias de estudo e 240 horas: 38 dias com duas matérias (76 sessões) e 2 dias fixos. O cronograma tem 236 blocos marcáveis.

## Limitações conhecidas

- A seleção de `FOCUS` é um critério editorial. Não existe levantamento estatístico público só das provas policiais do IDECAN; a escolha combina o número de questões de cada disciplina no edital, o perfil da banca descrito por cursos preparatórios e um levantamento de Processo Penal que mistura IDECAN e IBADE. Convém revisar a lista.
- O edital não informa quantas das 60 questões específicas são de cada disciplina. O tempo de cada matéria de peso 2 é proporcional à quantidade de aulas do curso, não ao peso na prova.
- A duração das aulas ainda não liberadas não aparece na plataforma. Os blocos dessas aulas foram agrupados por estimativa e podem passar de 1 hora.
- Não há folga para atrasos: as 76 sessões estão todas ocupadas. Não há sessão de revisão geral além do dia 22/01.
- Só o Simulado 02 entrou no cronograma. O Simulado 01 (módulo 12) ficou de fora por falta de horas.
- Ficaram fora, por menor prioridade (`LOW`): logaritmo (Matemática financeira), distribuições binomial negativa, multinomial e hipergeométrica (Estatística), análise tipológica e diagnóstico arquivístico (Arquivologia) e dois temas de redação. Mercadorias e impostos, CPC 16, depreciação e CPC 27 (Contabilidade) também estão em `LOW`, mas couberam em 21/01.
- Ficaram fora desde a versão anterior: aulas bônus de matemática básica (módulos 27, 28 e 52), Hardware (módulo 26, aulas 51 a 55), aulas 32 a 36 de Raciocínio Lógico e aulas 60 a 65 de Direito Administrativo.
- Não foi localizada aula para: séries temporais (Estatística) e arts. 209 a 212, 342 e 347 do Código Penal.
- 25/12/2026 e 01/01/2027 estão no cronograma como dias normais. Para retirá-los, inclua as datas na constante `OFF_EXTRA`; as sessões são redistribuídas e o que não couber aparece no quadro "Aulas fora do cronograma".
- O cronograma é fixo: blocos não marcados em dias passados são contados como atrasados, mas não são remarcados automaticamente.

## Publicar no GitHub e na Vercel

1. Crie um repositório vazio no GitHub.
2. Envie estes arquivos para a raiz do repositório (`git init`, `git add .`, `git commit -m "plano de estudos"`, `git remote add origin <url>`, `git push -u origin main`).
3. Na Vercel, clique em "Add New Project" e importe o repositório.
4. Em "Framework Preset" deixe "Other". Não preencha comando de build nem diretório de saída.
5. Clique em "Deploy". O endereço público fica pronto em alguns segundos.

## Ajustes comuns

- Início e fim do cronograma: constantes `START` e `LAST_WD`. Horas por dia: `SLOTS`. Horas por matéria: `PER`.
- Períodos sem estudo: lista `TRIPS`, com `from`, `to` (datas inclusivas) e `label`. Dias avulsos sem estudo: `OFF_EXTRA`.
- Aulas de peso 1 que entram no cronograma: objeto `FOCUS`, com a posição de cada aula na trilha (começa em 0 e segue a ordem em `TRACKS`). Para incluir uma aula, acrescente a posição dela.
- Blocos de menor prioridade: lista `LOW`, no formato `TRILHA.posição`.
- Aulas de cada trilha: lista `TRACKS`. Cada item é `[módulo, aulas e assunto, minutos de vídeo, data de liberação]`. Acrescentar um item ao final de uma trilha não altera as marcações já salvas; inserir ou remover no meio desloca as marcações daquela trilha.
- Matérias do cronograma e módulo de questões de cada uma: lista `GROUPS`.
- Prazo de cada trilha: constantes `P2` e `P1`.
- Dias com programação fixa (simulado e revisão final): objeto `FIXED`, uma entrada por data, com `[disciplina, módulo, o que fazer, horas]`.
- Nomes dos módulos do curso: objeto `MOD`. Texto "No curso" de cada disciplina: objeto `COURSE`.
- Data da prova: constante `EXAM`.
- Tópicos do edital: objeto `TOPICS` (a chave `RED` guarda os temas de redação, que também geram os blocos de redação de treino).
- Disciplinas, pesos e número de questões: objeto `SUBJ`; a ordem de exibição está em `SPEC`, `BASIC` e `ORDER`.
- Frases motivacionais: lista `QUOTES`.
- Animação do tiro: desenho em `GUN_SVG`, função `shoot` e os `@keyframes` `gun`, `flash`, `bullet`, `burst` e `spark` no CSS.
- Se o IDECAN alterar o cronograma do concurso, atualize a seção "Datas importantes" (função `renderTimeline`).

## Dados salvos

O progresso continua na chave `edital-pcac-oi-v3`. Os tópicos do edital já marcados são mantidos. As aulas já marcadas na versão anterior continuam marcadas, porque o identificador de cada aula não mudou; as marcações dos antigos blocos de sábado e de revisão deixam de aparecer. O botão "Reiniciar progresso" apaga tópicos, blocos e simulados.
