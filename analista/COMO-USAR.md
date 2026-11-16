# Como usar o Analista (sem programar)

## 1. Criar o analista (uma vez só)
1. Entre em **claude.ai** → menu lateral → **Projects** → **Create project**.
   Nome sugerido: "Analista Cavalos EUA".
2. Clique em **Set project instructions** (instruções do projeto) e cole todo o
   conteúdo de `instrucoes-do-analista.md`.
3. Em **Project knowledge** (arquivos), envie `docs/variaveis-analise-corridas-eua.md`.
   Ele serve de referência das variáveis e categorias.

## 2. Analisar uma corrida (todo dia)
1. Abra o racecard da corrida no site.
2. Envie o conteúdo para uma conversa nova dentro do projeto. Use uma destas formas:
   - **Copiar e colar o texto**: selecione a página (Ctrl+A), copie (Ctrl+C) e
     cole (Ctrl+V). É a forma mais precisa.
   - **Prints de tela**: tire prints de todas as partes do form (cavalos,
     últimas corridas, odds). Funciona bem no celular.
   - **PDF**: se o site oferecer "imprimir/baixar PDF" (Brisnet, DRF, Equibase).
3. Se puder, acrescente:
   - odds atuais e movimentação (Betfair / flucs)
   - condição da pista do dia e scratches (cavalos retirados)
   - se a corrida mudou de grama para dirt
4. Escreva: **"Analise esta corrida"**.

## 3. Medir os resultados
Copie cada indicação para a planilha `planilha-acompanhamento.csv` (ela abre
no Excel ou no Google Planilhas) e preencha o resultado real depois da corrida.
Depois de ~100 corridas dá para ver:
- % de acerto do vencedor e do lay
- em que tipo de corrida o analista vai melhor (dirt/turf, sprint/route, classe)
- se o lucro seria positivo com as odds reais

Com esses números, ajustamos as instruções (por exemplo: "evite lay em turf mole").

## 4. Fontes de dados de corridas dos EUA
| Fonte | Custo | O que oferece | Observação |
|---|---|---|---|
| **Punters.com.au** | Grátis | Form guide do seu uso atual | Use copiar/colar ou prints |
| **Equibase.com** | Grátis (entries/results); PPs pagas | Fonte oficial: inscritos, scratches, condição da pista, resultados | Ótimo para conferir dados e resultados |
| **Brisnet.com** | Pago por card (alguns dólares) | Past performances completas em PDF: Speed/Pace figures, estilo de corrida, workouts, stats de treinador | A fonte mais completa para este analista |
| **DRF.com** | Pago | PPs com Beyer Speed Figures | Padrão da indústria |
| **TwinSpires / Xpressbet** | PPs básicas grátis com conta | Past performances | Pode depender da disponibilidade no seu país |
| **Betfair** | Grátis com conta | Odds de back/lay e movimentação ao vivo | Necessário para o lay |

## 5. Dados do Equibase (recomendado)
Junto com o PDF do Punters, envie para cada corrida um print da página
**Entries** do Equibase (grátis). Ele mostra o que o Punters não mostra:
- preço de claiming e restrições da corrida (N2L, sem vitória desde X etc.);
- pesos reais e descontos de aprendiz;
- jockey atualizado;
- se a corrida era de grama e pode ter ido para a pista principal;
- medicação (Lasix) e mudança de equipamento (blinkers).

Em 10/11/26, com esses dados, o analista acertou 4 de 8 vencedores e 4 de 4 lays.
