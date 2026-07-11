## 🗓️ ROADMAP DE 20 DIAS — Julia Cafeteria

**Meta: sistema funcional até 03/08 (26 dias daqui, 20 de estudo intenso).**

Table

| Dia    | Foco            | O que fazer                                                                    | Notas de referência                               | [[Quick Guide Django]]                                                                          |
| :----- | :-------------- | :----------------------------------------------------------------------------- | :------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| **01** | Setup           | Instalar Python, venv, Django. Criar projeto e apps. Rodar `runserver`.        | 01-Instalação, 01-Projeto e App                   | - [[Quick Reference/Django/01 Fundamentos/Instalação\|Instalação]]<br>- [[Projeto e App]]<br>   |
| **02** | Models          | Mapear 9 tabelas do SQL para models. `inspectdb` + ajustes.                    | 02-Modelos, 02-Fields, 02-Relacionamentos         | - [[02 Models]]                                                                                 |
| **03** | Models          | `makemigrations`, `migrate`, testar no shell. Criar managers customizados.     | 02-Managers, 02-QuerySets                         | - [[Migrations]] <br>- [[Managers]]                                                             |
| **04** | Admin           | Registrar todos os models no Admin. Customizar list_display, filters, inlines. | 01-Django Admin                                   | - [[Django Admin]]                                                                              |
| **05** | URLs + Views    | Criar urls.py de cada app. Primeiras FBVs: listar cardápio, detalhe item.      | 03-Function Views, 03-Request e Response, 07-URLs | - [[Function Views]]<br>- [[Request e Response]]<br>- [[07 URLs]]                               |
| **06** | Templates       | Criar `base.html`, herança, partials. Listar cardápio com Bootstrap cards.     | 04-Sintaxe, 04-Herança, 10-Integração             | - [[Sintaxe]]<br> - [[Herança]]<br> - [[Integração]]                                            |
| **07** | Forms           | Criar ModelForm de ItemCardapio. View de criar/editar com crispy.              | 06-Forms, 06-ModelForm, 10-crispy-forms           | - [[Forms]]<br>- [[ModelForm]]<br>- [[crispy-forms]]                                            |
| **08** | CRUD Cardápio   | CRUD completo de itens (List, Create, Update, Delete).                         | 03-Generic Views, 15-CRUD Completo                | - [[Generic Views]]<br>- [[CRUD Completo]]                                                      |
| **09** | HTMX            | Adicionar HTMX: busca de itens sem reload, adicionar ao carrinho.              | 05-O que é, 05-hx-get, 05-Partial Templates       | - [[O que é]]<br>- [[hx-get e hx-post]]<br>- [[Partial Templates]]                              |
| **10** | Comandas        | Models de Mesa, Comanda, Pedido, ItemPedido. View de abrir comanda.            | 02-Relacionamentos, 03-Function Views             | - [[Quick Reference/Django/02 Models/Relacionamentos\|Relacionamentos]]<br>- [[Function Views]] |
| **11** | Fluxo Pedido    | Adicionar pedido à comanda com HTMX. Calcular total.                           | 05-hx-post, 05-hx-target, 06-FormSets             | - [[hx-get e hx-post]]<br>- [[hx-target e hx-swap]]<br>- [[FormSets]]                           |
| **12** | Fechamento      | Fechar comanda, calcular total, registrar no caixa. Signals.                   | 02-Signals, 15-Notificações com HTMX              | - [[Signals]]<br>- [[Notificações com HTMX]]                                                    |
| **13** | Caixa           | Lançamentos de entrada/saída. Relatório simples do dia.                        | 09-Annotations, 09-Aggregations                   | - [[Annotations e Aggregations]]                                                                |
| **14** | Auth            | Custom User, login/logout, permissões por função.                              | 08-Auth, 08-Custom User Model                     | - [[Authorization]]<br>- [[Authentication]]<br>- [[Custom User Model]]                          |
| **15** | Dashboard       | KPIs: mesas ocupadas, comandas abertas, total do dia.                          | 15-Dashboard, 09-F() e Q()                        | - [[Dashboard]]<br>- [[F() e Q() Objects]]                                                      |
| **16** | Busca + Filtros | Busca de itens, filtros por categoria, por data.                               | 15-Busca, 15-Filtros Avançados                    | - [[Quick Reference/Django/15 Casos Comuns/Busca\|Busca]]<br>- [[Filtros Avançados]]            |
| **17** | Testes          | Testes de models, views, forms.                                                | 11-TestCase, 11-Client                            | - [[TestCase]]<br>- [[Client]]                                                                  |
| **18** | Performance     | `select_related`, `prefetch_related`, cache de views.                          | 12-Query Optimization, 12-Caching                 | - [[Query Optimization]]<br>- [[Caching]]                                                       |
| **19** | Segurança       | CSRF, XSS, SQL Injection, validações. Revisão geral.                           | 13-Segurança                                      | - [[13 Segurança]]                                                                              |
| **20** | Deploy          | Preparar para Kinghost. `collectstatic`, WhiteNoise, mod_wsgi.                 | 14-Deploy, 14-Kinghost                            | - [[14 Deploy]]<br>- [[Kinghost]]                                                               |

**Dias 21-26**: Buffer para ajustes, correções de bugs, e polimento.

---

## 🎯 Regras de ouro para os 20 dias

1. **Um dia, um foco**. Não tente fazer tudo de uma vez.
2. **Código todo dia**, mesmo que 30 minutos. Momentum é tudo.
3. **Teste no shell** antes de escrever a view. `python manage.py shell` é seu laboratório.
4. **Commit no Git** todo dia. Se quebrar, você volta.
5. **Não perfeccionismo**. Funcional > bonito. Bonito vem depois.
6. **Cheat Sheet aberto**. Quando travar, consulta. Não decora.
7. **Pergunta quando travar**. Não fique 3 horas em um erro sozinho.