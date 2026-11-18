# Plano de Estudos · Oficial Investigador de Polícia (PC-AC)

Dashboard estático em HTML, CSS e JavaScript puros, sem dependências nem etapa de build. Baseado no Edital nº 001/2026 SEAD/PCAC (banca IDECAN) e na grade do curso "Combo PC AC - Oficial Investigador de Polícia - Pós-Edital" (Direito Simples e Objetivo, Hotmart), levantada em 11/11/2026. Cronograma refeito em 15/11/2026, com a retirada das disciplinas de Direito e o registro das aulas já assistidas.

A página tem duas partes principais. O cronograma distribui as aulas do curso em 6 horas por dia, de segunda a sexta, com duas matérias por dia. O edital checklist lista o conteúdo programático, disciplina por disciplina, e informa em qual módulo do curso cada disciplina está. Ao marcar um bloco ou um tópico, uma pistola 2D dispara contra a caixa de seleção. Em cada sessão de hoje ou de dias futuros há um botão "Substituir", que permite estudar outra matéria no lugar daquela. O progresso e as substituições são salvos no navegador (localStorage).

## Foto da aluna

A ilustração em pixel art da aluna fica no arquivo `oficial.png`, na raiz do projeto, e aparece no topo da página, ao lado do título. O arquivo tem a resolução nativa da pixel art, 71 x 124 pixels (16 KB). Ele foi reconstruído a partir da imagem original, um JPG de 1167 x 2000 pixels em que cada pixel da arte media cerca de 16,2 pixels.

A imagem é exibida em múltiplos inteiros do tamanho do arquivo, para os pixels ficarem nítidos e iguais: 3 vezes no computador (213 x 372) e 2 vezes no celular, até 480 pixels de tela (142 x 248), com `image-rendering: pixelated`. O tamanho fica na regra `.avatar` do CSS e na regra de mesmo nome dentro de `@media (max-width:480px)`.

Para trocar a imagem, substitua `oficial.png` por outra com o mesmo nome. Se a nova imagem tiver outro tamanho, atualize os atributos `width` e `height` da tag `<img class="avatar">` e as larguras e alturas da regra `.avatar`, sempre em múltiplos inteiros do tamanho do arquivo. Use a pixel art na resolução nativa, e não uma versão ampliada: ampliada, a imagem é reduzida pelo navegador e os pixels ficam borrados e desiguais. Ajuste também o texto alternativo (`alt`) da tag, que descreve a imagem para leitores de tela.

## Como o cronograma é montado

O cronograma vai de 16/11/2026 a 22/01/2027 (sexta-feira antes da prova) e é calculado pela função `buildPlan` a partir das listas `TRACKS` e `GROUPS`.

- Duas matérias por dia, 3 horas cada. Em cada matéria, as duas primeiras horas são de aulas novas e a terceira é de questões do mesmo assunto (módulos QAP 2.0 e Exercícios de Fixação).
- Ordem das aulas: dentro de cada matéria, as aulas seguem a ordem dos módulos na plataforma. Uma aula só entra em um dia igual ou posterior à data em que fica disponível. As aulas com "Estreia 14/11/2026" usam a constante `E`; as aulas com data no título usam essa data.
- Escolha das matérias do dia: cada matéria acumula um crédito diário proporcional ao número de sessões que ainda precisa; as duas com mais crédito viram as matérias do dia. As de peso 2 recebem 20% a mais de crédito, para terminarem antes.
- Matérias de cálculo: Estatística, Matemática financeira e Raciocínio Lógico nunca caem no mesmo dia.
- Peso 2: Contabilidade (com Matemática financeira), Estatística, TI, Análise de Dados, Arquivologia e Administração entram completas e terminam até 14/01/2027.
- Peso 1: só entram as aulas listadas em `FOCUS`. Português, Informática e Raciocínio Lógico têm de três a quatro sessões cada. Realidade do Acre e Legislação Institucional têm duas sessões cada.
- Direito: Direito Constitucional, Direito Administrativo, Processo Penal e o restante de Direito Penal foram retirados do cronograma e do checklist. Ficou apenas a trilha `RM`, dos crimes contra o respeito aos mortos (Código Penal, arts. 209 a 212), com duas sessões: uma de leitura da lei e fichamento e outra de revisão e questões. O curso não tem aula desses artigos, por isso os blocos são de estudo pelo texto da lei.
- Legislação penal especial: trilha `LPE`, com as três leis penais especiais que o edital lista para o cargo de Oficial Investigador na disciplina Noções de Direito Penal e Processual Penal: Tortura (Lei 9.455/1997), Abuso de autoridade (Lei 13.869/2019) e Identificação criminal (Lei 12.037/2009). São sete blocos de leitura do texto compilado, com fichamento e quadro comparativo, em quatro sessões. O curso não tem aula dessas leis. A lista de 36 leis penais e processuais penais especiais do Anexo III (Lei de Drogas, Organizações Criminosas, Lavagem, Maria da Penha etc.) pertence ao cargo de Delegado e não foi incluída.
- Aulas já assistidas (lista `SEEN`): Estatística 01 e 02, Informática 01 a 06 e 16, Contabilidade 01 a 03 e Raciocínio Lógico 03 e 04. Não entram no cronograma e aparecem no quadro "Aulas já assistidas e aulas fora do cronograma". Como a aula 03 de Contabilidade foi vista inteira, o bloco seguinte passou a conter só a aula 04.
- Redação: quatro blocos de aula e seis redações de treino, em cinco sessões; a terceira hora de cada sessão é de correção pelos critérios do edital.
- Viagem: de 09/12/2026 a 22/12/2026 não há estudo (constante `TRIPS`). Nas duas semanas seguintes, a primeira hora de questões de cada matéria já iniciada é de revisão do que foi visto antes da viagem.
- Dias fixos (objeto `FIXED`): 15/01/2027 tem o Simulado 02 do curso (5 horas) e 1 hora de correção; 22/01/2027 é de revisão final.
- Se sobrar sessão, entram os blocos de `LOW` e, depois, sessões de revisão por questões. Com a trilha `LPE`, todos os blocos de `LOW` ainda couberam, e não sobrou sessão para revisão por questões.

Com a viagem, são 40 dias de estudo e 240 horas: 38 dias com duas matérias (76 sessões) e 2 dias fixos. O cronograma tem 236 blocos marcáveis.

## Substituir a matéria do dia

Ao lado do nome de cada matéria, nos dias de hoje em diante, há o botão "Substituir". Ele abre a lista de matérias que podem ser estudadas no lugar daquela sessão. Cada opção é a próxima sessão de outra matéria, trazida para o dia escolhido.

A substituição troca o dono de duas vagas do cronograma: a vaga do dia passa para a matéria escolhida, e a vaga de onde essa matéria saiu passa para a matéria retirada. Depois, cada matéria ocupa as suas vagas na ordem original das aulas. Por isso nenhuma aula é pulada nem fica fora de ordem: as sessões seguintes da matéria retirada avançam uma vaga cada.

Só aparecem as opções que respeitam as regras do cronograma: aula já liberada na data, a mesma matéria só uma vez por dia, no máximo uma matéria de cálculo por dia (Estatística, Matemática financeira e Raciocínio Lógico) e aulas de peso 2 até 14/01 e de peso 1 até 21/01. Os dias passados, os dias fixos (15/01 e 22/01) e os dias da viagem não podem ser alterados. Os blocos já marcados acompanham a sessão quando ela muda de dia.

Na mesma lista aparecem as aulas fora do cronograma: as de peso 1 fora do foco e os temas de redação que não couberam. Cada opção traz as duas próximas aulas já liberadas daquela matéria, com uma hora de questões. Como são conteúdo a mais, cada uma tira do plano uma das quatro sessões de menor prioridade do fim do cronograma (20/01 e 21/01: Contabilidade, Estatística, Matemática financeira e Arquivologia), que passa para o quadro "fora do cronograma". A matéria retirada segue a ordem das aulas e fica com a vaga da sessão que saiu. Por isso o limite é de quatro trocas desse tipo, e elas só funcionam no lugar de matérias de peso 1 ou dessas próprias sessões de menor prioridade: as de peso 2 passariam do prazo de 14/01. O resumo do cronograma mostra quantas ainda cabem. As disciplinas de Direito retiradas do plano não estão nessa lista, porque o código não tem as aulas delas.

O dia em que a troca foi feita mostra a etiqueta "matéria substituída" e o botão "Desfazer"; os demais dias que mudaram por causa dela mostram "ajustado por substituição". O resumo do cronograma tem o botão "Desfazer as substituições de hoje em diante". Desfazer uma substituição pode desfazer também as feitas depois dela que dependiam dela; nesse caso a página avisa. A desfeita é recusada se alterar um dia que já passou.

O código fica na seção `SUBSTITUIÇÃO DE MATÉRIAS` do script (funções `sessOf`, `initSlots`, `swapOwn`, `fill`, `problem`, `planFrom`, `options`, `extraSess`, `extraOptions`, `lowLeft`, `subBox` e `undoAdj`). As substituições são aplicadas sobre o resultado de `buildPlan`, sem recalcular o algoritmo, para que os dias anteriores não mudem.

## Limitações conhecidas

- A seleção de `FOCUS` é um critério editorial. Não existe levantamento estatístico público só das provas policiais do IDECAN; a escolha combina o número de questões de cada disciplina no edital, o perfil da banca descrito por cursos preparatórios e um levantamento de Processo Penal que mistura IDECAN e IBADE. Convém revisar a lista.
- O edital não informa quantas das 60 questões específicas são de cada disciplina. O tempo de cada matéria de peso 2 é proporcional à quantidade de aulas do curso, não ao peso na prova.
- A duração das aulas ainda não liberadas não aparece na plataforma. Os blocos dessas aulas foram agrupados por estimativa e podem passar de 1 hora.
- Legislação penal especial: o edital pode ter sido alterado por leis recentes (a Lei 12.037/2009 e a Lei 9.455/1997 aparecem com alterações de 2025 e 2026 em fontes secundárias). Os blocos mandam conferir a redação atual no texto compilado do Planalto; o conteúdo dessas alterações não foi verificado nesta versão.
- Risco de eliminação: Direito Constitucional (3 questões) e Direito Administrativo (3 questões) não têm nenhuma hora no plano, e a disciplina de Direito Penal e Processual Penal (6 questões) está reduzida aos arts. 209 a 212. O edital exige ao menos 1 ponto em cada disciplina; acertar essas questões passa a depender de conhecimento anterior da aluna.
- Não há sessões de revisão por questões no cronograma atual. A folga são as quatro sessões de menor prioridade de 20/01 e 21/01, que também são consumidas quando a aluna traz aulas de fora do cronograma.
- Só o Simulado 02 entrou no cronograma. O Simulado 01 (módulo 12) ficou de fora por falta de horas.
- Os blocos de menor prioridade (`LOW`) entraram todos no fim do cronograma: logaritmo (Matemática financeira), distribuições binomial negativa, multinomial e hipergeométrica (Estatística), análise tipológica e diagnóstico arquivístico (Arquivologia), mercadorias e impostos, CPC 16, depreciação e CPC 27 (Contabilidade) e os dois últimos temas de redação.
- Ficaram fora desde a versão anterior: aulas bônus de matemática básica (módulos 27, 28 e 52), Hardware (módulo 26, aulas 51 a 55) e aulas 32 a 36 de Raciocínio Lógico.
- Não foi localizada aula para: séries temporais (Estatística) e arts. 209 a 212 do Código Penal.
- 25/12/2026 e 01/01/2027 estão no cronograma como dias normais. Para retirá-los, inclua as datas na constante `OFF_EXTRA`; as sessões são redistribuídas e o que não couber aparece no quadro "Aulas fora do cronograma".
- Blocos não marcados em dias passados são contados como atrasados e não são remarcados automaticamente. A substituição de matéria só reorganiza dias de hoje em diante e não cria horas: não resolve um dia inteiro sem estudo.
- A substituição só traz a próxima sessão de cada matéria, e a matéria retirada fica com a vaga da escolhida. Por isso algumas trocas não aparecem: por exemplo, se a vaga liberada cair em um dia com outra matéria de cálculo, ou se a aula seguinte da matéria escolhida ainda não estiver liberada.
- As substituições são salvas por navegador. Quem abrir o plano em outro aparelho não as verá.

## Publicar no GitHub e na Vercel

1. Crie um repositório vazio no GitHub.
2. Envie estes arquivos para a raiz do repositório, incluindo `oficial.png` (`git init`, `git add .`, `git commit -m "plano de estudos"`, `git remote add origin <url>`, `git push -u origin main`).
3. Na Vercel, clique em "Add New Project" e importe o repositório.
4. Em "Framework Preset" deixe "Other". Não preencha comando de build nem diretório de saída.
5. Clique em "Deploy". O endereço público fica pronto em alguns segundos.

## Ajustes comuns

- Início e fim do cronograma: constantes `START` e `LAST_WD`. Horas por dia: `SLOTS`. Horas por matéria: `PER`.
- Períodos sem estudo: lista `TRIPS`, com `from`, `to` (datas inclusivas) e `label`. Dias avulsos sem estudo: `OFF_EXTRA`.
- Aulas já assistidas: lista `SEEN`, no formato `TRILHA.posição`. Para registrar outra aula já vista, acrescente o identificador do bloco.
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

O progresso continua na chave `edital-pcac-oi-v3`. Os tópicos do edital já marcados são mantidos. As aulas já marcadas na versão anterior continuam marcadas, porque o identificador de cada aula não mudou; as marcações das disciplinas de Direito retiradas deixam de aparecer; as marcações dos antigos blocos de sábado e de revisão deixam de aparecer. As substituições de matéria ficam no campo `adj` da mesma chave. Se uma alteração no código tornar alguma substituição inválida, ela é descartada ao abrir a página. O botão "Reiniciar progresso" apaga tópicos, blocos, substituições e simulados.
