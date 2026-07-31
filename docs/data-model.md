# Modelagem de Dados

## Entidades

### Pedido (orders)
| Coluna | Tipo | Descrição |
|---|---|---|
| id | String (UUID) | Identificador do pedido |
| customer | String | Nome do cliente |
| status | String | Status do pedido (padrão "open") |
| created_at | DateTime | Data de criação |

### Item (items)
| Coluna | Tipo | Descrição |
|---|---|---|
| id | String (UUID) | Identificador do item |
| order_id | String | Referência ao pedido (FK) |
| sku | String | Código do produto |
| description | String | Descrição do item |
| quantity | Integer | Quantidade |

## Relacionamento
Um pedido tem vários itens (1:N). Ao excluir um pedido, os itens dele são excluídos junto (cascade).

## Como as tabelas são criadas
As tabelas são criadas automaticamente pelo SQLAlchemy a partir dos modelos em `app/models.py`, sem uso de migrations nesta etapa.
