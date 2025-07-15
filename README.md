# Análise de Evasão de Clientes - Telecom X

## Introdução
Este projeto realiza uma análise exploratória de dados (EDA) e o processo de ETL (Extração, Transformação e Carregamento) para investigar os fatores associados à evasão de clientes (churn) na Telecom X, uma empresa de telecomunicações. O objetivo é identificar padrões que influenciam a decisão de cancelamento dos serviços, fornecendo insights para estratégias de retenção. A análise utiliza dados de um arquivo JSON hospedado em [TelecomX_Data.json](https://raw.githubusercontent.com/alura-cursos/challenge2-data-science/refs/heads/main/TelecomX_Data.json) e foi implementada em Python com as bibliotecas `pandas`, `matplotlib`, `seaborn` e `plotly`.

## Objetivo
- **Problema**: A Telecom X enfrenta uma alta taxa de churn, impactando seus custos e receita.
- **Solução**: Realizar ETL para preparar os dados e conduzir uma EDA para identificar padrões relacionados ao churn, como tipo de contrato, método de pagamento, tempo de contrato (`tenure`) e gastos mensais (`Charges.Monthly`).
- **Resultados**: Gerar visualizações e um relatório com insights e recomendações para reduzir a evasão.

## Pré-requisitos
Para reproduzir a análise, você precisa de:
- Python 3.8+
- Bibliotecas Python:
  ```bash
  pip install pandas matplotlib seaborn plotly requests numpy
  ```
- Conexão à internet para acessar o arquivo JSON.

## Estrutura do Projeto
- `telecom_x_etl_eda.py`: Script principal que realiza o ETL, a EDA e gera o relatório.
- `relatorio_telecom_x.md`: Relatório detalhado em Markdown com o processo e os resultados.
- Gráficos gerados:
  - `churn_distribution.png`: Proporção de churn.
  - `tenure_vs_churn.png`: Tempo de contrato por churn.
  - `monthlycharges_vs_tenure.html`: Gráfico interativo de valor mensal vs. tempo.
  - `correlation_matrix.png`: Matriz de correlação.
  - `contract_vs_churn.png`: Tipo de contrato por churn.
  - `monthlycharges_distribution.png`: Distribuição de gastos mensais por churn.

## Como Executar
1. Clone o repositório:
   ```bash
   git clone <URL_DO_REPOSITORIO>
   cd <NOME_DO_REPOSITORIO>
   ```
2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```
3. Execute o script principal:
   ```bash
   python telecom_x_etl_eda.py
   ```
4. Verifique os arquivos gerados:
   - Relatório: `relatorio_telecom_x.md`
   - Gráficos na pasta do projeto.

## Processo ETL
### Extração
- Os dados foram extraídos de um arquivo JSON via API usando `requests.get`.
- O JSON foi carregado em um DataFrame com `pd.read_json`.

### Transformação
- **Desaninhamento**: Colunas aninhadas (`customer`, `phone`, `internet`, `account`) foram desaninhadas com `pd.json_normalize`.
- **Padronização**: Hífens foram removidos de `Contract` e `customerID`; texto convertido para minúsculas.
- **Conversão de Tipos**: `Charges.Total` convertido de string para float; `Churn` mapeado para binário (0 = Não, 1 = Sim).
- **Valores Ausentes**: 11 valores nulos em `Charges.Total` substituídos por 0; linhas com `Churn` vazio removidas.
- **Duplicatas**: Removidas com base em `customerID`.

### Carregamento
- O DataFrame tratado foi usado para gerar visualizações e o relatório em Markdown.

## Análise Exploratória (EDA)
A EDA examinou variáveis categóricas e numéricas para identificar padrões de churn:
1. **Proporção de Churn**: 26.5% dos clientes churnaram.
2. **Tipo de Contrato**: Contratos "month to month" têm maior churn (42%) comparado a "one year" (11%) e "two year" (3%).
3. **Método de Pagamento**: "Electronic check" apresenta alta taxa de churn (45%).
4. **Tempo de Contrato (`tenure`)**: Clientes com menos de 12 meses churnam mais.
5. **Gastos Mensais (`Charges.Monthly`)**: Clientes com gastos mais altos (mediana ~80) são mais propensos a churnar.
6. **Total Gasto (`Charges.Total`)**: Baixos valores, associados a baixo `tenure`, correlacionam-se com churn.

### Gráficos Gerados
- **Proporção de Churn**: Gráfico de pizza (`churn_distribution.png`).
- **Churn por Contrato**: Gráfico de barras (`contract_vs_churn.png`).
- **Churn por Método de Pagamento**: Gráfico de barras (`paymentmethod_vs_churn.png`).
- **Distribuição de Tenure**: Histograma (`tenure_vs_churn.png`).
- **Distribuição de Charges.Monthly**: Box plot e histograma (`monthlycharges_distribution.png`).
- **Charges.Total e Tenure**: Box plots, histogramas e gráficos de densidade.

## Conclusão
A análise identificou que:
- Clientes com contratos "month to month", métodos de pagamento "electronic check", baixo `tenure` (<12 meses) e altos `Charges.Monthly` (~80) têm maior probabilidade de churn.
- Clientes com maior `tenure` e `Charges.Total` elevado tendem a permanecer.

## Recomendações
1. **Incentivar Contratos Longos**: Oferecer descontos para contratos de um ou dois anos.
2. **Melhorar Pagamentos**: Simplificar o processo de "electronic check" ou incentivar métodos automáticos.
3. **Focar no Onboarding**: Suporte proativo para clientes novos (<12 meses).
4. **Revisar Preços**: Ajustar planos com altos `Charges.Monthly` para melhorar a percepção de valor.
5. **Segmentação**: Direcionar campanhas para clientes de alto risco (ex.: baixo `tenure`, "electronic check").
6. **Monitoramento**: Criar um painel para acompanhar métricas de churn.

## Contribuições
Contribuições são bem-vindas! Para sugerir melhorias:
1. Faça um fork do repositório.
2. Crie uma branch (`git checkout -b feature/nova-funcionalidade`).
3. Commit suas alterações (`git commit -m 'Adiciona nova funcionalidade'`).
4. Envie para o repositório (`git push origin feature/nova-funcionalidade`).
5. Abra um Pull Request.

## Licença
Este projeto está licenciado sob a [MIT License](LICENSE).