# Statistical Analysis of Federal Highway Accidents in Brazil (Datatran 2024)

Statistical analysis and exploratory data modeling on federal highway traffic incidents using R, Tidyverse, and reproducible R Markdown reporting, aimed at evidence-based public safety and traffic enforcement.

---

## 1. Problema de Negócio e Contexto

No âmbito da gestão de segurança pública e infraestrutura viária, a redução de sinistros e de letalidade nas rodovias federais depende diretamente da capacidade analítica de alocar efetivo e radares em locais e horários de maior criticidade:

1. **Alocação Intuitiva vs. Baseada em Evidências:** Sem a exploração sistemática dos microdados, a fiscalização viária corre o risco de ser orientada por intuição operacional, concentrando patrulhas em trechos secundários enquanto pontos de alto atrito e letalidade permanecem desassistidos.
2. **Multifatorialidade dos Sinistros:** Acidentes graves resultam da convergência de múltiplos fatores: falhas humanas (ex.: reação tardia, velocidade incompatível), características da via (pista simples, curvas sinuosas) e adversidades climáticas (chuva, neblina).

O objetivo deste projeto foi conduzir uma auditoria estatística rigorosa sobre o conjunto oficial de microdados da Polícia Rodoviária Federal (`datatran2024.csv`), estruturando relatórios reprodutíveis para:
- Mapear a concentração de acidentes e letalidade por unidade federativa e eixo rodoviário.
- Diagnosticar as causas primárias de sinistros e correlacioná-las à severidade das vítimas.
- Subsidiar o planejamento operacional de intervenção preventiva e fiscalização ostensiva.

---

## 2. Processo e Racional das Escolhas Técnicas

### 2.1. Ecossistema R & Tidyverse (`dplyr`, `ggplot2`, `tidyr`)
- **Manipulação Declarativa Funcional:** A utilização do pipeline (`%>%`) com `dplyr` viabilizou transformações encadeadas legíveis, com agregações dimensionais por causa de acidente, UF, severidade e traçado de pista sem mutabilidade desordenada de variáveis em memória.
- **Gramática de Gráficos (`ggplot2`):** A separação entre dados, mapeamento estético e camadas geométricas permitiu produzir visualizações estatísticas de alta precisão técnica (gráficos de barras reordenados, distribuições horárias e faceting de severidade).

### 2.2. Higienização e Tratamento de Dados Públicos
- **Tratamento de Codificação e Delimitadores:** Microdados governamentais brasileiros comumente utilizam delimitadores de ponto e vírgula (`;`) e codificação `latin1`. O carregamento foi configurado via `read.csv(..., sep = ";", fill = TRUE, encoding = "latin1")` para evitar truncamento de caracteres e erros de parsing.
- **Normalização de Severidade:** Separação e tratamento unificado de feridos leves, feridos graves e óbitos, calculando taxas relativas de letalidade por tipo de colisão em vez de considerar apenas contagens brutas.

### 2.3. R Markdown como Padrão de Reprodutibilidade
- A consolidação de código e documentação em `projeto_analise_dados.Rmd` assegura que toda a análise estatística seja 100% auditável e reprodutível, gerando relatórios em PDF/HTML diretamente a partir do código fonte.

---

## 3. Resultados Atingidos e Métricas de Validação

### 3.1. Diagnósticos de Causalidade e Severidade
- **Concentração de Causas Primárias:** Constatou-se que causas ligadas à conduta humana (como reação tardia do condutor, desatenção e velocidade incompatível) lideram com folga o volume total de ocorrências.
- **Índice de Letalidade por Tipo de Sinistro:** Colisões frontais e atropelamentos de pedestres apresentaram taxas de letalidade substancialmente superiores a colisões traseiras ou saídas de pista, indicando prioridade de fiscalização em trechos de ultrapassagem proibida em pista simples.

### 3.2. Padrões Espaciais e Temporais
- **Picos Horários:** Concentração pronunciada de sinistros graves nos finais de tarde e inícios de noite (entre 17h e 20h), coincidindo com transição de luminosidade e cansaço de condutores.
- **Concentração Rodoviária:** Identificação de eixos rodoviários troncais responsáveis por percentual desproporcional das vítimas fatais, servindo de métrica direta para recalibração de rondas operacionais.

---

## 4. Arquitetura da Solução e Estrutura

```text
projeto-integrado-ciencia-de-dados/
├── datatran2024.csv                      # Microdados oficiais de acidentes (PRF 2024)
├── projeto_analise_dados.Rmd              # Notebook R Markdown reprodutível com todo o pipeline
├── MANIPULAÇÃO E ANÁLISE DE DADOS COM R.pdf # Relatório estatístico compilado
├── docs/                                 # Documentações complementares de apoio
├── img/                                  # Gráficos exportados para relatórios executivos
└── LICENSE                               # Licença MIT
```

---

## 5. Como Executar

### 5.1. Pré-requisitos
- R (versão 4.0 ou superior)
- RStudio Desktop (recomendado) ou ambiente CLI com Rscript

### 5.2. Instalação de Pacotes no R

Abra o console do R ou RStudio e execute:
```r
install.packages(c("dplyr", "ggplot2", "tidyr", "rmarkdown", "knitr"))
```

### 5.3. Execução e Compilação do Relatório

1. Clone o repositório:
```bash
git clone https://github.com/RicsonRamos/projeto-integrado-ciencia-de-dados.git
cd projeto-integrado-ciencia-de-dados
```

2. Para compilar o relatório completo em PDF ou HTML via terminal:
```bash
Rscript -e "rmarkdown::render('projeto_analise_dados.Rmd', output_format = 'pdf_document')"
```

3. Alternativamente, abra o arquivo `projeto_analise_dados.Rmd` no RStudio e clique em **Knit**.
