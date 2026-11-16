# Analista de Corridas de Cavalos (EUA): variáveis e roteiro

Este documento cobre o turfe **de galope (Thoroughbred) nos Estados Unidos**.
Ele lista as variáveis que contam para a análise, explica o que é diferente no
turfe americano e mostra os passos para construir o analista.

---

## 0. O que muda nos EUA

| Tema | Nos EUA | Efeito na análise |
|---|---|---|
| Apostas | **Pari-mutuel** (pool/tote). Não há odd fixa | A odd "final" só existe depois da largada e ainda muda durante a corrida (late money, CAW: computer-assisted wagering) |
| Odd de abertura | **Morning Line (M/L)**: estimativa do handicapper do hipódromo, não é preço de mercado | Use como prior. A informação de mercado vem do tote |
| "Rating" | Não há rating oficial como o do BHA (Reino Unido). Usam-se **figuras de velocidade** | Beyer (DRF), Brisnet Speed/Pace, Equibase Speed Figure, Timeform US, Thoro-Graph, Ragozin |
| Peso | Faixa estreita (≈ 115–126 lb), exceto nos handicaps | Pesa menos que na Europa. O desconto do aprendiz ("bug") importa mais |
| Medicação | Lasix (furosemida) aparece nas PPs. Regras HISA/estaduais limitam o uso no dia da corrida (2 anos e stakes) | "First-time Lasix" é um padrão clássico. Confira a regra vigente |
| Pistas | Maioria em **dirt**, com turf e sintético | A troca de superfície é uma das variáveis mais fortes |
| Takeout | ≈ 15–25 % conforme o tipo de aposta e o estado | O modelo precisa superar essa margem para ter lucro |

---

## 1. Categorias (classes) de corrida nos EUA

Da mais baixa para a mais alta:

1. **Maiden Claiming (MCL)**: cavalos sem vitória que podem ser reclamados (comprados) pelo preço da corrida.
2. **Maiden Special Weight (MSW)**: cavalos sem vitória, sem preço de reclamação. É bem mais forte que o MCL.
3. **Claiming (CLM)**: todos à venda pelo preço declarado (ex.: $5k, $10k, $25k, $50k…). **O preço é a medida de classe.**
   - Variantes: *non-winners of 2 lifetime* (N2L), *N3L*, *N1Y* (sem vitória no ano) etc.
4. **Starter Allowance / Starter Optional Claiming**: para cavalos que já correram por um certo preço de claiming.
5. **Allowance (ALW)**: com condições como N1X (sem vitória fora maiden/claiming), N2X, N3X.
6. **Optional Claiming (AOC / OC)**: allowance em que o cavalo pode entrar com ou sem preço de reclamação.
7. **Stakes**:
   - Ungraded / Listed
   - **Grade 3 → Grade 2 → Grade 1** (G1 é o topo: Kentucky Derby, Breeders' Cup etc.)
8. **Handicap**: peso definido pelo secretário de corridas conforme a qualidade do cavalo.

Restrições que costumam vir junto com a classe:
- **Idade**: 2yo, 3yo, 3yo+, 4yo+
- **Sexo**: Fillies (F), Fillies & Mares (F&M), aberto
- **Statebred** (ex.: NY-bred, CA-bred, FL-bred): campos mais fracos que os "open"
- **Bolsa (purse)**: mostra a qualidade real entre hipódromos. Um $25k claiming em Saratoga ≠ um $25k claiming em Penn National.

---

## 2. Variáveis por grupo

As variáveis que você citou estão marcadas com ★. As demais são acréscimos.

### 2.1 Corrida (contexto)
| Variável | Observação |
|---|---|
| ★ Distância | Em furlongs. **Sprint** (< 1 milha, em geral 5f–7f) × **Route** (≥ 1 milha). Uma curva × duas curvas |
| ★ Hipódromo | Configuração (oval de 1 milha ou 1⅛), tamanho da reta, viés típico |
| ★ Tipo de terreno | **Dirt**, **Turf**, **Sintético** (Tapeta, Polytrack) |
| Condição da pista | Dirt: fast, good, muddy, sloppy, wet-fast, *sealed*. Turf: firm, good, yielding, soft |
| **Off-the-turf** | Corrida de turf transferida para o dirt. Muitos scratches. Cavalos "MTO" (main track only) |
| ★ Categoria / classe | Ver seção 1. Inclua o preço de claiming e a purse |
| ★ Dia da semana | Fins de semana têm cards melhores e pools maiores. Dias de semana têm campos mais fracos |
| Hora/posição no card | Primeiras corridas × feature race |
| Tamanho do campo | Altera probabilidades, dinâmica de ritmo e valor |
| Clima / temperatura / vento | Afetam a condição da pista |
| **Track bias do dia** | Viés de velocidade (speed bias) ou de raia (rail/outside) observado nas corridas anteriores do mesmo dia |
| Estação / meet | Saratoga, Del Mar, Keeneland etc. têm padrões próprios. Começo e fim de meet também |

### 2.2 Cavalo: identidade e físico
| Variável | Observação |
|---|---|
| ★ Sexo | Colt, horse, gelding, filly, mare. **Primeira corrida após castração** (first-time gelding) é um sinal |
| Idade | Evolução física, sobretudo aos 2 e 3 anos |
| ★ Peso carregado | Inclui o desconto do aprendiz (bug: em geral 10/7/5 lb, varia por estado) |
| Linhagem (pedigree) | Pai/mãe e avô materno. Essencial para estreantes, estreia em turf, pista pesada, distância nova. Ex.: Tomlinson ratings |
| Leilão / preço de venda | Proxy de qualidade para estreantes |
| Statebred | Pode correr em provas restritas |

### 2.3 Desempenho passado (Past Performances)
| Variável | Observação |
|---|---|
| ★ Resultado das últimas corridas | Posição **e distância batida (beaten lengths)**. Isso vale mais que só a colocação |
| ★ "Rating" → **Figuras de velocidade** | Última, melhor das 3 últimas, média, tendência (subindo/caindo), figura na mesma superfície/distância |
| Figuras de ritmo (pace) | Brisnet E1, E2, Late Pace. Frações (¼, ½, ¾) |
| Pontos de chamada | Posição em cada chamada. Mostra o estilo de corrida |
| **Estilo de corrida** | E (front-runner), E/P, P (stalker), S (closer) |
| **Cenário de ritmo** | Quantos "E" estão no campo. Um único speed solitário costuma ser muito forte |
| Trip notes / comentários | "Bumped start", "wide trip", "steadied". Uma corrida com problema esconde o potencial real |
| Mudança de classe | Subida/queda (claiming price, purse, categoria). **Queda após vitória** ou **queda acentuada** pode indicar problema físico |
| Mudança de superfície/distância | Dirt→turf, sprint→route, primeira vez em sintético |
| Recorde na pista/distância/superfície | Linhas "Life / Track / Dist / Surface" das PPs |
| Consistência | % de vitórias e de top-3 na carreira |
| Ganhos (earnings) | Por largada |

### 2.4 Condicionamento e forma
| Variável | Observação |
|---|---|
| ★ Dias sem correr | Layoff (> 45–60 d, > 180 d). Também ciclo: "2nd off layoff", "3rd off layoff" |
| **Workouts (treinos)** | Muito importantes nos EUA: frequência, tempo, ranking ("bullet" = melhor tempo do dia), gate works |
| Número de corridas no ciclo | Cavalo "em forma" × "gasto" |
| Equipamento | Blinkers on/off (**first-time blinkers**), bandagens, mudança de ferradura |
| Medicação | Lasix (first-time, on/off), Bute |
| **Reclamado recentemente** | "First off the claim": o novo treinador costuma melhorar o cavalo |

### 2.5 Pessoas (connections)
| Variável | Observação |
|---|---|
| ★ Jockey | % de vitórias no meet e no ano, por hipódromo e superfície. **Troca de jockey** (para um melhor) |
| Treinador | % geral e **por padrão (angle)**: layoff, first-time starter, first off claim, turf debut, blinkers on, class drop. Os dados das PPs (Brisnet/DRF) trazem esses números |
| Combo jockey–treinador | % de vitórias juntos |
| Proprietário | Grandes stables, uso de agentes |

### 2.6 Largada
| Variável | Observação |
|---|---|
| Post position (raia/gate) | Viés por hipódromo × distância (ex.: raias externas em sprints de 1 curva de turf) |
| Scratches | Mudam o campo e o cenário de ritmo |
| Also-eligibles | Lista de reserva |

### 2.7 Mercado (odds)
| Variável | Observação |
|---|---|
| ★ Odd de abertura → **Morning Line** | Opinião do handicapper, não do mercado |
| Primeira odd do tote | Primeiro pool registrado |
| ★ Odd final | Só se conhece **após a largada**. Use-a para treinar e avaliar o modelo, nunca como entrada na hora de apostar |
| ★ Movimentação de odds (flucs) | No pari-mutuel: série temporal do tote (M/L → abertura → 10 min → 2 min → final). "Late money", diferença entre M/L e tote, proporção do pool de win × exacta probables. Atenção: os CAW movem as odds até depois do "off" |
| Probabilidade implícita | 1/(odd+1) normalizada para tirar o takeout |
| Favorito / posição no ranking de odds | Feature relativa |

### 2.8 Features relativas (as mais importantes para o modelo)
Uma corrida é uma **competição**. Valores absolutos importam menos que a
comparação com os rivais **da mesma corrida**:
- Figura de velocidade − melhor figura do campo
- Ranking da figura dentro da corrida
- Z-score de cada variável dentro da corrida
- Número de rivais com estilo "E" (pressão de ritmo)

---

## 3. Roteiro de construção

### Etapa 1: definir o objetivo
- **Probabilidade de vitória** de cada cavalo (recomendado) → depois comparar com o mercado para encontrar **valor** (overlay).
- Comece com um escopo fechado, por exemplo **um circuito** (NYRA, Califórnia, Kentucky, Gulfstream) e **uma superfície** (dirt). Expanda depois.

### Etapa 2: obter os dados
| Fonte | Conteúdo | Observação |
|---|---|---|
| **Brisnet** (Data Files `.DRF`, "Single File") | PPs completas em CSV (~1.400 campos/cavalo): figuras, pace, workouts, stats de treinador/jockey | Barato por card. É o formato mais usado em projetos de programação |
| **Equibase** | Dados oficiais, charts de resultado | Os termos proíbem scraping. Feeds são pagos |
| DRF Formulator | PPs com Beyer | Uso interativo |
| Timeform US, TrackMaster | Figuras alternativas | |
| Hipódromos / tote | Odds em tempo real e will-pays | Para os flucs: grave snapshots periódicos você mesmo |

> Para treinar o modelo você precisa de **histórico** (ideal ≥ 1–2 anos de um
> circuito): PPs *antes* da corrida + resultado *depois*. Sem isso o modelo não aprende.

### Etapa 3: banco de dados
Tabelas sugeridas: `hipodromos`, `corridas`, `inscricoes` (cavalo na corrida),
`past_performances`, `workouts`, `cavalos`, `jockeys`, `treinadores`,
`odds_snapshots`, `resultados`.

### Etapa 4: engenharia de features
- Calcular as features da seção 2, sobretudo as **relativas** (2.8).
- **Sem vazamento (leakage)**: toda feature deve usar só informação disponível *antes* da corrida.

### Etapa 5: modelo
1. **Baseline**: probabilidade implícita das odds finais. Bater o mercado é difícil e é a referência real.
2. **Logit condicional / multinomial** (abordagem de Bill Benter): estima a probabilidade de cada cavalo dentro da corrida.
3. **Gradient boosting** (LightGBM/XGBoost) com objetivo de ranking ou classificação + **calibração**.
4. **Modelo combinado**: o modelo fundamental mais as odds do mercado num 2º estágio (Benter).

### Etapa 6: validação
- Divisão **temporal** (treina no passado, testa no futuro), nunca aleatória.
- Métricas: log-loss, Brier, calibração, **ROI simulado já descontado o takeout**.

### Etapa 7: aposta e gestão de banca
- Apostar só quando `prob_modelo × (odd + 1) > 1` com margem de segurança.
- **Kelly fracionado** (¼ ou ½ Kelly).
- Lembre que, no pari-mutuel, a sua própria aposta reduz a odd.

### Etapa 8: interface do "analista"
- Pipeline Python que lê o card do dia → gera features → calcula probabilidades → produz um relatório por corrida.
- Opcional: uma camada de LLM (Claude) que lê as PPs e o resultado do modelo e escreve uma análise em texto (cenário de ritmo, angles, cavalos de valor).
