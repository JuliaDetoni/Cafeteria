## O problema do roadmap anterior

| Falha                                | Por quê                                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------------------- |
| **Dia 2-3: "Mapear 9 tabelas"**      | `inspectdb` faz isso em 10 minutos. O resto do dia fica vazio.                               |
| **Dia 4: Só Admin**                  | Admin é ferramenta interna, não é tela do sistema.                                           |
| **Dia 5: "Primeiras FBVs"**          | Uma listagem e um detalhe levam 30 minutos se os models estão prontos.                       |
| **Dia 8: "CRUD Cardápio"**           | Só cardápio? E comanda, mesa, funcionário, caixa?                                            |
| **Dia 10: "Comandas"**               | Só agora? A comanda é o **core do negócio**. Deveria vir antes.                              |
| **Dia 14: Auth**                     | Auth deveria vir no dia 1 — sem login, não há contexto de funcionário/mesa.                  |
| **Dia 17: Testes**                   | Testes são importantes, mas em 20 dias com deadline, são luxo.                               |
| **Nenhum dia para "Cozinha"**        | O pedido sai da comanda, vai para a cozinha, volta pronto. Esse fluxo não existe no roadmap. |
| **Nenhum dia para "ajustes e bugs"** | 20 dias sem buffer é ilusão.                                                                 |

---

## O princípio correto: **telas primeiro, Django depois**

Você não precisa saber o que é `select_related` para abrir uma comanda. Você precisa de uma tela que mostre mesas livres, um botão "Abrir", e um redirect. O Django aprendido na prática, resolvendo problemas reais da cafeteria.

> [!important] A cafeteria tem 5 áreas de operação
> Cada área precisa de telas. O roadmap deve distribuir tempo entre elas, não entre conceitos do Django.

---

## Roadmap revisado: 20 dias — Julia Cafeteria

### Semana 1: Fundação + Cardápio + Auth (Dias 1-5)

| Dia | Foco | Telas do dia | O que aprende de Django |
|-----|------|--------------|------------------------|
| **01** | Setup + Auth | Login, Logout | venv, startproject, startapp, settings, `django.contrib.auth`, `LoginView`, `LogoutView` |
| **02** | Cardápio (listar) | Listagem de itens, busca por nome | `ListView` ou FBV, `filter()`, `icontains`, templates, Bootstrap cards |
| **03** | Cardápio (CRUD) | Criar, editar, excluir item | `CreateView`, `UpdateView`, `DeleteView`, `ModelForm`, crispy-forms |
| **04** | Mesas | Painel de mesas (livre/ocupada/reservada), ocupar mesa | `choices`, `save()` override, signals (mesa ocupada → comanda aberta) |
| **05** | Funcionários | Listar, cadastrar funcionário | Mesmo padrão de CRUD, reforço |

> [!note] Por que Auth no dia 1?
> Sem login, não há "funcionário que abriu a comanda". O contexto de usuário é essencial para todo o resto. `django.contrib.auth` já resolve 90% — não precisa de Custom User agora.

---

### Semana 2: Comandas + Pedidos + Cozinha (Dias 6-12)

| Dia | Foco | Telas do dia | O que aprende de Django |
|-----|------|--------------|------------------------|
| **06** | Abrir comanda | Selecionar mesa livre, criar comanda | `ForeignKey`, `CreateView` com dados pré-preenchidos, `messages` |
| **07** | Comanda ativa | Ver comanda, adicionar pedido (form) | `DetailView`, `ModelForm` com `initial`, `form_valid()` |
| **08** | Pedido com HTMX | Adicionar item sem reload, listar itens do pedido | HTMX `hx-post`, `hx-target`, partial templates, `render_block` |
| **09** | Cozinha | Fila de pedidos pendentes, marcar como pronto | `filter(status='Pendente')`, `UpdateView` com HTMX, `hx-swap="outerHTML"` |
| **10** | Fechar comanda | Calcular total, selecionar forma de pagamento | `annotate`, `Sum`, transações com `transaction.atomic` |
| **11** | Histórico | Listar comandas fechadas, buscar por data | `filter`, `date` lookup, paginação |
| **12** | Ajustes | Buffer para bugs, refinamentos, polimento | — |

> [!tip] Dia 8 é o coração do sistema
> Adicionar pedido com HTMX é onde tudo se conecta: models (ItemPedido), forms (quantidade + observação), views (processar POST), templates (partial para injetar na lista). Se esse dia funcionar, o resto é repetição.

---

### Semana 3: Caixa + Dashboard + Deploy (Dias 13-20)

| Dia | Foco | Telas do dia | O que aprende de Django |
|-----|------|--------------|------------------------|
| **13** | Caixa (lançamentos) | Registrar entrada/saída, listar do dia | Mesmo padrão de CRUD, `DateTimeField`, `default=timezone.now` |
| **14** | Caixa (fechamento) | Fechar caixa do dia, saldo | `aggregate(Sum)`, `annotate`, filtros por data |
| **15** | Dashboard | KPIs: mesas ocupadas, total do dia, itens mais vendidos | `Count`, `Sum`, `values`, `order_by`, gráficos simples (Bootstrap progress bars) |
| **16** | Relatórios | Exportar CSV de vendas, filtro por período | `HttpResponse` com `content_type='text/csv'`, `csv.writer` |
| **17** | Perfis | Editar perfil, trocar senha | `UpdateView` com `request.user`, `PasswordChangeView` |
| **18** | Testes + segurança | Revisão geral, CSRF, validações | `TestCase` básico, `@login_required`, `@permission_required` |
| **19** | Deploy | Preparar para Kinghost, `collectstatic`, WhiteNoise | `settings/production.py`, `ALLOWED_HOSTS`, `DEBUG=False` |
| **20** | Buffer | Bugs, ajustes finais, documentação | — |

## Regra de ouro para os 20 dias

> **"Hoje eu quero ver a tela X funcionando. O Django que me ensine como."**

Não: "Hoje eu vou estudar Generic Views."  
Sim: "Hoje eu quero criar um item no cardápio. Vou usar CreateView porque é rápido."

O aprendizado vem como **efeito colateral** de construir. Não como objetivo.

---
