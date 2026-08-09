# ADR 001 — Escolher estratégia de deploy Kubernetes

**Status:** Aceito  
**Data:** 2026-08-05

## Contexto

A aplicação precisa ser executada em ambiente de nuvem com disponibilidade,
padronização de deploy e possibilidade de evolução futura. Era necessário
escolher uma estratégia para executar os containers da aplicação.

As principais restrições eram manter o custo reduzido, utilizar os recursos
disponíveis na Magalu Cloud e permitir automação através do GitHub Actions.

## Alternativas consideradas

- **K3s em VM na Magalu Cloud** — solução Kubernetes leve, compatível com
  manifests Kubernetes tradicionais, menor custo operacional e adequada para
  ambientes de aprendizado e projetos menores. Exige gerenciamento da VM.

- **MKS (Kubernetes Gerenciado da Magalu Cloud)** — oferece maior abstração,
  gerenciamento do cluster pelo provedor e maior facilidade operacional.
  Possui custo maior.

- **Docker Compose em VM** — solução simples e com menor complexidade inicial,
  porém sem recursos nativos de orquestração, escalabilidade e gerenciamento
  de réplicas.

## Decisão

Foi escolhido o uso de K3s em uma VM na Magalu Cloud.

O critério principal foi equilibrar custo, aprendizado e capacidade de utilizar
os mesmos conceitos do Kubernetes utilizado em ambientes profissionais.

A aplicação foi configurada com duas réplicas através de um Deployment,
permitindo maior disponibilidade do serviço.

## Consequências

**Positivas:**

- Uso de uma solução compatível com Kubernetes padrão.
- Baixo custo de infraestrutura.
- Possibilidade de utilizar Deployments, Services e outros recursos Kubernetes.
- Facilita uma futura migração para Kubernetes gerenciado.

**Negativas:**

- A manutenção da VM e do cluster é responsabilidade da equipe.
- Menor disponibilidade comparado a um cluster gerenciado com alta disponibilidade.
- Exige conhecimento de Kubernetes para operação.