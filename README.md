# Formação-em-Análise-de-Dados-com-Excel-e-IA

# Bella's Investiment Table

## Sobre o projeto

A **Bella's Investiment Table** é uma ferramenta desenvolvida no Excel 2019 para simular a evolução de um patrimônio por meio de aportes mensais. A planilha permite informar o valor investido por mês, o prazo em anos e o perfil de investimento, calculando o patrimônio projetado e uma estimativa de dividendos mensais.

O projeto foi desenvolvido a partir da comparação com a planilha **Tabela do professor**, buscando ampliar a simulação com perfis de investimento, distribuição percentual da carteira e cálculo automático da taxa mensal de acordo com o perfil escolhido.

## 1. Quais perguntas a ferramenta responde e onde encontrar as respostas?

As perguntas são respondidas na aba `Simulador`, na seção **Investimento Mensal**.

| Pergunta | Célula | Funcionamento |
|---|---|---|
| Quanto investir por mês? | `E25` | Permite informar o aporte mensal. |
| Por quantos anos? | `E26` | Define o prazo da simulação em anos. |
| Qual a taxa de rendimento mensal? | `E28` | Busca automaticamente a taxa correspondente ao perfil selecionado em `E21`. |
| Quanto de patrimônio vai acumular? | `E29` | Calcula o patrimônio futuro considerando os aportes mensais, o prazo, a taxa e o patrimônio inicial. |
| Quanto vai receber de dividendos por mês? | `E30` | Estima os dividendos mensais multiplicando o patrimônio projetado pela taxa mensal selecionada. |

### Informações complementares

A planilha também apresenta a seção **Capital para investimento**, que contém:

- `E19`: salário mensal;
- `E20`: aporte mensal recomendado, calculado como 30% do salário;
- `E21`: perfil de investimento selecionado.

A célula `E27` permite informar um patrimônio inicial, que também participa do cálculo do patrimônio futuro.

## 2. Como as funções VF e PROCV entram nos cálculos?

### Função VF — Valor Futuro

A função `VF` calcula o valor futuro de um investimento com base na taxa de rendimento por período, no número de períodos, nos aportes e no capital inicial.

Na planilha, a fórmula de `E29` é:

```excel
=VF(taxa;anos*12;-aporte_mensal;-patrimonio_inicial)
```

Os argumentos representam:

- `taxa`: taxa de rendimento mensal;
- `anos*12`: conversão do prazo de anos para meses;
- `-aporte_mensal`: aporte realizado mensalmente;
- `-patrimonio_inicial`: capital que já existe no início da simulação.

Os sinais negativos são utilizados para representar os valores investidos como saídas de dinheiro, permitindo que a função retorne o patrimônio futuro positivo.

### Função PROCV — Pesquisa Vertical

A função `PROCV` localiza o perfil escolhido na tabela de referência e retorna a taxa mensal correspondente.

Na célula `E28`, a fórmula utilizada é:

```excel
=PROCV(E21;B:F;5;FALSO)
```

Como funciona:

1. `E21` contém o perfil selecionado.
2. `B:F` corresponde à tabela que contém os perfis e suas taxas.
3. `5` indica que o resultado deve vir da quinta coluna do intervalo, ou seja, da coluna `F`.
4. `FALSO` exige uma correspondência exata do perfil.

Dessa forma, ao alterar o perfil em `E21`, a taxa mensal em `E28` é atualizada automaticamente.

### Cálculo dos dividendos mensais

A célula `E30` utiliza a fórmula:

```excel
=E29*E28
```

Ela multiplica o patrimônio projetado pela taxa mensal selecionada.

**Limitação da simulação:** essa fórmula estima uma renda mensal usando a taxa de rendimento total como se fosse uma taxa de distribuição de dividendos. Para estimar dividendos de maneira mais realista, seria necessário criar uma taxa de dividendos específica, independente da rentabilidade total da carteira.

## 3. Intervalos nomeados utilizados

Os intervalos nomeados permitem utilizar nomes descritivos nas fórmulas, facilitando a leitura e a manutenção da planilha.

Todos os intervalos abaixo estão definidos na aba `Simulador`.

| Nome definido | Referência | Finalidade |
|---|---|---|
| `anos` | `Simulador!$E$26` | Prazo do investimento em anos. |
| `aporte_mensal` | `Simulador!$E$25` | Valor investido mensalmente. |
| `patrimonio_inicial` | `Simulador!$E$27` | Capital inicial da simulação. |
| `taxa` | `Simulador!$E$28` | Taxa mensal selecionada para os cálculos. |
| `taxa_mensal` | `Simulador!$E$28` | Outro nome para a mesma célula da taxa mensal. |
| `patrimonio_projetado` | `Simulador!$E$29` | Resultado do cálculo do patrimônio futuro. |
| `dividendo_mensal` | `Simulador!$E$30` | Resultado da estimativa de dividendos mensais. |
| `salario` | `Simulador!$E$19` | Salário mensal informado. |
| `Perfil` | `Simulador!$B$11` | Cabeçalho da coluna de perfis. |
| `Conservador` | `Simulador!$B$12` | Célula com o nome do perfil Conservador. |
| `Moderado` | `Simulador!$B$13` | Célula com o nome do perfil Moderado. |
| `Arrojado` | `Simulador!$B$14` | Célula com o nome do perfil Arrojado. |

Os nomes `taxa` e `taxa_mensal` apontam para a mesma célula. Já os nomes dos perfis apontam para as células que contêm seus rótulos na tabela, e não para as linhas completas.

## 4. Percentuais de cada perfil e origem dos valores

A tabela de perfis está localizada no intervalo `B11:G14` da aba `Simulador`.

| Perfil | Renda fixa | FIIs | Ações e ETFs | Taxa mensal simulada |
|---|---:|---:|---:|---:|
| Conservador | 90% | 0% | 10% | 0,5% |
| Moderado | 60% | 25% | 15% | 0,7% |
| Arrojado | 30% | 30% | 40% | 0,9% |

### Origem dos percentuais

Os percentuais de distribuição foram definidos como exemplos ilustrativos durante a elaboração da ferramenta, considerando diferentes níveis de exposição a classes de investimento.

- **Conservador:** maior concentração em renda fixa e menor exposição à renda variável.
- **Moderado:** distribuição intermediária entre renda fixa, fundos imobiliários e ações ou ETFs.
- **Arrojado:** maior exposição a fundos imobiliários, ações e ETFs.

As taxas mensais de 0,5%, 0,7% e 0,9% também foram definidas como parâmetros hipotéticos para permitir a simulação automática.

Esses valores não foram obtidos de uma série histórica ou de uma fonte oficial de rentabilidade. São premissas didáticas utilizadas para demonstrar o funcionamento das fórmulas. A rentabilidade efetiva varia conforme os produtos, o período, os custos, os impostos e as condições de mercado.

Os percentuais de cada carteira totalizam 100%. Na versão atual da planilha, os 10% restantes do perfil Conservador estão classificados como ações e ETFs, conforme a tabela implementada.

## 5. O que mudou em relação à ferramenta do professor?

A ferramenta original, disponível na planilha `Tabela do professor`, já permite informar um aporte mensal, um prazo e uma taxa mensal, além de calcular o patrimônio acumulado e os dividendos mensais.

A Bella's Investiment Table mantém essa ideia central e acrescenta uma organização própria para a simulação.

| Característica | Tabela do professor | Bella's Investiment Table |
|---|---|---|
| Aporte mensal | Informado pelo usuário. | Informado pelo usuário, com sugestão de aporte de 30% do salário. |
| Prazo | Informado em anos. | Informado em anos. |
| Taxa mensal | Informada diretamente. | Buscada automaticamente conforme o perfil selecionado. |
| Patrimônio inicial | Não é considerado explicitamente na fórmula principal de patrimônio. | Pode ser informado em `E27` e incluído no cálculo. |
| Patrimônio futuro | Calculado pela função `VF`. | Calculado pela função `VF`, considerando o patrimônio inicial. |
| Dividendos mensais | Calculados com base no patrimônio e no rendimento da carteira. | Estimados a partir do patrimônio projetado e da taxa mensal selecionada. |
| Perfis de investimento | A planilha apresenta uma distribuição de FIIs por perfil, incluindo Conservador, Moderado e Agressivo. | Apresenta os perfis Conservador, Moderado e Arrojado, com percentuais para renda fixa, FIIs e ações ou ETFs. |
| Distribuição da carteira | Detalhamento por tipo de fundo imobiliário, em uma segunda aba. | Distribuição por classes de investimento na tabela principal de perfis. |
| Cenários de prazo | Apresenta projeções para 2, 5, 10, 20 e 30 anos. | Calcula o patrimônio para o prazo informado pelo usuário. |
| Intervalos nomeados | Utiliza nomes como `aporte`, `qtd_anos`, `taxa_mensal` e `patrimonio`. | Utiliza nomes descritivos como `aporte_mensal`, `anos`, `patrimonio_inicial` e `patrimonio_projetado`. |

### Principais melhorias

1. **Seleção por perfil:** a taxa mensal passa a ser obtida automaticamente com `PROCV`.
2. **Inclusão de patrimônio inicial:** a projeção considera o capital já acumulado, além dos aportes futuros.
3. **Organização por classes de investimento:** os percentuais são apresentados em uma tabela de fácil consulta.
4. **Sugestão de aporte:** a planilha calcula uma referência de investimento mensal# Bella's Investments 💰

## Sobre o projeto

A **Bella's Investments** é uma ferramenta desenvolvida no Excel 2019 para simular a evolução de um patrimônio por meio de aportes mensais. A planilha permite informar o valor investido por mês, o prazo do investimento, o patrimônio inicial e o perfil de investimento.

Com essas informações, a ferramenta calcula o patrimônio futuro estimado e apresenta uma estimativa de dividendos mensais, utilizando uma taxa de distribuição separada da taxa de rendimento da carteira.

O projeto foi desenvolvido a partir da comparação com a ferramenta **Tabela do professor**, com o objetivo de personalizar as simulações, organizar os perfis de investimento e automatizar os cálculos.

## 1. Quais perguntas a ferramenta responde?

Na aba `Simulador`, a seção **Capital para investimento** apresenta as informações relacionadas ao salário e ao perfil selecionado. A seção **Investimento Mensal** concentra os dados e os resultados da simulação.

| Pergunta | Célula | Como a resposta é obtida |
|---|---|---|
| Quanto investir por mês? | `E25` | Valor do aporte mensal informado pelo usuário. |
| Por quantos anos? | `E26` | Prazo da simulação em anos. |
| Qual a taxa de rendimento mensal? | `E28` | Taxa obtida automaticamente conforme o perfil escolhido em `E21`. |
| Quanto de patrimônio vai acumular? | `E29` | Valor futuro calculado com a função `VF`, considerando o aporte mensal, o prazo, a taxa e o patrimônio inicial. |
| Quanto vai receber de dividendos por mês? | `E30` | Estimativa calculada pela multiplicação do patrimônio projetado pela taxa de dividendos mensal. |

### Informações complementares

Na seção **Capital para investimento**:

- `E19`: salário mensal informado.
- `E20`: aporte mensal recomendado, calculado como 30% do salário.
- `E21`: perfil de investimento selecionado.

Na seção **Investimento Mensal**:

- `E27`: patrimônio inicial informado pelo usuário.
- `E31`: taxa de dividendos mensal correspondente ao perfil selecionado.

A planilha também apresenta um gráfico de porcentagem de ativos por perfil para facilitar a visualização da distribuição das classes de investimento.

## 2. Como as funções VF e PROCV são utilizadas?

### Função VF — Valor Futuro

A função `VF` calcula o patrimônio projetado ao final do período de investimento, considerando os aportes mensais e o capital inicial.

Na célula `E29`, a fórmula é:

```excel
=VF(E28;E26*12;-E25;-E27)
```

Os argumentos são:

- `E28`: taxa de rendimento mensal.
- `E26*12`: prazo em meses, convertido a partir dos anos.
- `-E25`: aporte mensal.
- `-E27`: patrimônio inicial.

Os sinais negativos representam os valores investidos como saídas de dinheiro, permitindo que o resultado do patrimônio futuro seja apresentado como um valor positivo.

O cálculo pressupõe uma taxa mensal constante durante todo o período, com aportes regulares. Por isso, o resultado é uma projeção matemática, e não uma garantia de rentabilidade.

### Função PROCV — Pesquisa Vertical

A função `PROCV` procura o perfil selecionado e retorna a taxa correspondente na tabela de referência.

Na célula `E28`, a fórmula é:

```excel
=PROCV(E21;$B$12:$H$14;5;FALSO)
```

Ela procura o perfil informado em `E21` na primeira coluna do intervalo `B12:H14` e retorna o valor da quinta coluna desse intervalo, correspondente à taxa de rendimento mensal simulada na coluna `F`.

Na célula `E31`, a fórmula é:

```excel
=PROCV(E21;$B$12:$H$14;7;FALSO)
```

Nesse caso, a função retorna o valor da sétima coluna do intervalo, correspondente à taxa de dividendos mensais na coluna `H`.

O argumento `FALSO` exige uma correspondência exata do perfil selecionado.

Dessa forma, ao alterar o perfil entre Conservador, Moderado e Arrojado, as duas taxas são atualizadas automaticamente.

### Cálculo dos dividendos mensais

Na célula `E30`, a fórmula utilizada é:

```excel
=E29*E31
```

O cálculo multiplica o patrimônio projetado pela taxa de dividendos mensal.

Essa fórmula permite separar a estimativa de dividend

P.S. Perfis: os percentuais são premissas ilustrativas, não recomendações financeiras validadas.
