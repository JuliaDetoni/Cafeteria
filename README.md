## 🗺️ Roadmap de Aprendizado (Python + SQL)

Vamos fazer **6 módulos**, cada um com um **entregável concreto** (checkpoint).  
Você vai sempre usar **seu próprio banco** como laboratório.  
Não precisa seguir linearmente – pode pular ou repetir. O importante é **brincar com os dados**.

---

### 📌 Módulo 0 – Setup e ferramentas (pré-requisito)
- Instalar MySQL Server (se já não tiver) ou usar o XAMPP/Docker com seu dump.
- Instalar Python + bibliotecas:  
  `pip install mysql-connector-python pandas matplotlib seaborn jupyter`
- Conectar o Python ao banco (script de teste).

**Checkpoint 0:**  
Um script `.py` ou notebook `.ipynb` que conecta no banco e mostra o nome de todas as tabelas.

---

### 📌 Módulo 1 – SQL puro (consultas básicas e intermediárias)
- **Objetivo:** responder perguntas de negócio só com SQL.
- **Tópicos:** `SELECT`, `WHERE`, `JOIN` (2+ tabelas), `GROUP BY`, `HAVING`, `ORDER BY`, funções de agregação (`SUM`, `COUNT`, `AVG`).

**Checkpoint 1 (entregável):**  
Um arquivo `.sql` (ou uma célula no notebook) com as seguintes consultas:

1. Listar todas as comandas abertas hoje com o nome do funcionário responsável e o número da mesa.  
2. Faturamento bruto do dia 13/05/2025 (somente entradas `PDV` da `tbl_caixa`).  
3. Top 5 itens mais vendidos (em quantidade) no mês de maio/2025 (use `tbl_item_pedido`).  
4. Média de tempo entre `entrada_pedido` e `saida_pedido` por categoria de produto.  

> *Se não souber alguma, tudo bem – a gente resolve junto.*

---

### 📌 Módulo 2 – SQL avançado (subconsultas, window functions, views)
- **Objetivo:** extrair insights mais sofisticados.
- **Tópicos:** Subconsultas `IN`/`EXISTS`, `WITH` (CTE), `ROW_NUMBER()`, `RANK()`, criar `VIEW`.

**Checkpoint 2:**  
Criar uma **view** chamada `vw_relatorio_gerencial` que responda, numa única consulta:

- Por dia:  
  - total de vendas (valor líquido, desconsiderando calotes)  
  - total de despesas operacionais  
  - lucro do dia  
  - ticket médio por comanda  

> Dica: vai precisar unir `tbl_caixa` (entradas e saídas) e `tbl_comanda`.

---

### 📌 Módulo 3 – Python básico + conexão com BD
- **Objetivo:** executar queries do Python e tratar os resultados como listas/dicionários.
- **Tópicos:** `mysql.connector`, tratamento de `None`, laços `for`, f-strings, list comprehension.

**Checkpoint 3:**  
Um script Python que:
1. Pergunte ao usuário uma data (ex: `'2025-05-13'`).
2. Execute a query do faturamento bruto daquele dia (igual ao checkpoint 1).
3. Exiba na tela: `"Faturamento em YYYY-MM-DD: R$ X.XXX,XX"`.
4. Se não houver vendas, mostre `"Nenhum movimento"`.

---

### 📌 Módulo 4 – Análise de dados com pandas
- **Objetivo:** carregar resultados de queries em DataFrames e manipular.
- **Tópicos:** `pd.read_sql()`, `groupby`, `merge`, `pivot_table`, tratamento de datas.

**Checkpoint 4:**  
Carregar a view `vw_relatorio_gerencial` (do módulo 2) em um DataFrame. Em seguida:

- Gerar uma tabela pivô mostrando **total de vendas por dia da semana** (segunda, terça…).
- Plotar um gráfico de barras simples com `matplotlib` das vendas ao longo dos dias (mesmo que poucos dias, serve para aprender).

---

### 📌 Módulo 5 – Visualização e storytelling
- **Objetivo:** criar dashboards simples e responder perguntas hipotéticas.
- **Tópicos:** `matplotlib`, `seaborn`, gráficos de linha, barras, pizza.

**Checkpoint 5:**  
Fazer um **pequeno relatório em PDF ou imagem** (pode ser notebook exportado) contendo:

1. Um gráfico de linha do **faturamento diário** nos primeiros 15 dias de maio (vai precisar gerar datas – pode simular dados novos ou usar o que existe).
2. Gráfico de barras horizontais mostrando os **5 funcionários que mais atenderam** (número de pedidos).
3. Gráfico de pizza da **distribuição de formas de pagamento** (dinheiro, pix, cartão) apenas para vendas PDV.

> Dica: você pode inserir dados fictícios no banco para enriquecer as análises – isso é prática ótima de `INSERT`.

---

### 📌 Módulo 6 – Pequena automação (API ou agendamento)
- **Objetivo:** tornar uma análise recorrente automática.
- **Tópicos:** criar um script que roda um relatório e envia por e-mail (ou salva arquivo .csv em pasta).

**Checkpoint 6 (desafio final):**  
Um script Python que:

- Conecta ao banco.
- Executa a view gerencial.
- Salva o resultado num arquivo `relatorio_dia_{hoje}.csv`.
- Envia (simula) um e-mail com esse arquivo anexado – pode ser só um print "E-mail enviado para gerencia@cafeteria.com".

> Se quiser algo mais leve: agendar com `schedule` ou `cron` para rodar todo dia às 23h.

---

## 🎯 Próximos passos imediatos (sugestão)

1. **Rode o dump** no seu MySQL (se já não rodou).  
2. **Abra o MySQL Workbench** ou DBeaver e faça algumas consultas manuais – veja se os dados fazem sentido para você.  
3. **Me diga com qual módulo quer começar!**  
   - Se você já sabe um pouco de SQL, podemos pular para o módulo 1.  
   - Se quer treinar muito SQL, vamos fundo no módulo 2.  
   - Se já manja de SQL e quer meter Python, vamos direto ao módulo 3.
