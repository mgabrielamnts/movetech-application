# ADR 002 — Usar DBaaS PostgreSQL da Magalu Cloud

**Status:** Aceito

**Data:** 2026-08-04

## Contexto

A aplicação precisa de persistência de dados para armazenar pedidos e itens. 
Os dados devem permanecer disponíveis mesmo após reinicializações ou substituições
dos containers da aplicação.

Além disso, como a API possui múltiplas réplicas, o banco de dados precisa ser
acessível simultaneamente pelas diferentes instâncias da aplicação.

## Alternativas consideradas

- **DBaaS PostgreSQL gerenciado:** oferece gerenciamento da infraestrutura do banco,
backup e manutenção pelo provedor, reduzindo a complexidade operacional.

- **PostgreSQL executado em container no cluster:** teria menor dependência de um
serviço externo, porém exigiria gerenciamento de armazenamento persistente,
backups, atualizações e recuperação em caso de falhas.

## Decisão

Utilizar o **PostgreSQL gerenciado (DBaaS) da Magalu Cloud** como banco de dados
da aplicação.

A conexão com o banco é fornecida à aplicação por meio da variável de ambiente
`DATABASE_URL`, armazenada como um Secret no Kubernetes.

O principal critério para a escolha foi separar a persistência de dados do ciclo
de vida dos containers e reduzir a responsabilidade de administração do banco.

## Consequências

### Positivas

- Os dados permanecem independentes do ciclo de vida dos Pods.
- Múltiplas réplicas da API podem acessar o mesmo banco.
- Redução da complexidade de administração da infraestrutura do PostgreSQL.
- Maior facilidade para realizar manutenção e evolução da aplicação.

### Negativas

- Custo adicional pelo uso de um serviço gerenciado.
- Dependência da disponibilidade do serviço DBaaS.
- Menor controle sobre algumas configurações da infraestrutura do PostgreSQL.
