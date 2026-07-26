# Erick Mendelski

Engenheiro de software líder na **Qa+**, onde defino stack, arquitetura e prioridade técnica dos produtos digitais do grupo. Trabalho com sistemas financeiros multi-tenant: ERP, checkout, conciliação e migração de dados contábeis.

Antes disso: hub de pagamentos e order book cripto (Navi), checkout e coprodução (TheMembers), pagamento em eventos (Yuzer). Desde 2018 o assunto é o mesmo, software onde dinheiro não pode sumir.

[![PHP](https://img.shields.io/badge/PHP-8.x-777BB4?style=flat-square&logo=php&logoColor=white)](#)
[![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20?style=flat-square&logo=laravel&logoColor=white)](#)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)](#)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](#)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=black)](#)
[![Node.js](https://img.shields.io/badge/Node.js-20-5FA04E?style=flat-square&logo=nodedotjs&logoColor=white)](#)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)](#)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-erick--mendelski-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/erick-mendelski/)

---

## No que trabalho hoje

- Direção técnica dos produtos digitais do grupo Qa+, respondendo por arquitetura, disponibilidade, performance e custo de nuvem em produção.
- Infraestrutura híbrida: VMs em datacenter nacional para o legado e Laravel Cloud para os produtos novos.
- Domínio recorrente: multi-tenant, integração de PDV e ERP, checkout, conciliação e migração de dados contábeis.
- Fora do expediente, mantenho o **SmartPalace** em produção, um PMS hoteleiro multi-tenant de autoria própria, com assistente de IA integrado.

---


## Como eu trabalho

Não parto da premissa de que a primeira resposta está certa. Parto da premissa de que ela ainda não foi suficientemente testada.

- **Procuro primeiro validar as decisões, onde e como uma decisão pode falhar.** Antes de escolher uma arquitetura, uma regra de negócio ou uma implementação, tento encontrar os cenários que a quebram. Se continua fazendo sentido depois disso, aí sim ela vira código.
- **Código não é a única evidência.** README, documentação, comentários e até testes podem estar errados. Sempre que algo importante precisa ser provado, vou até a fonte: banco de dados, API real, logs, comportamento da aplicação ou documentação oficial.
- **Uso IA como uma ferramenta técnica, não como um oráculo.** Ela acelera pesquisa, gera hipóteses e encontra pontos cegos, mas nenhuma resposta entra no projeto sem confronto com a documentação oficial ou com experimentos reproduzíveis. Quanto mais convincente parece uma resposta, mais ela merece ser verificada.
- **Automatizo tudo que não quero depender da memória das pessoas.** Convenções importantes viram testes. Regras arquiteturais viram CI. O objetivo é que o repositório saiba dizer quando algo está errado, sem depender de alguém lembrar durante um code review.
- **Prefiro uma verdade reproduzível a uma opinião bem escrita.** Sempre que apresento um número, uma conclusão ou uma decisão técnica, procuro deixar claro de onde ela veio e como qualquer pessoa pode chegar ao mesmo resultado.

---

## Projetos

| Projeto | O que é | Stack |
|---|---|---|
| **[newsletter-api-laravel12](https://github.com/Mendelski/newsletter-api-laravel12)** | API de publicação por tópicos com entrega assíncrona confiável: fan-out em lote, entrega idempotente por chave única no banco, retry com backoff, dead-letter e rate limit por provedor. Cada afirmação do README aponta o teste que falha se ela deixar de ser verdade. | Laravel 12 · PHP 8.4 · PostgreSQL · Redis · Pest 4 |
| **[ai-chatbot](https://github.com/Mendelski/ai-chatbot)** | Bot de WhatsApp com Gemini multimodal: transcreve áudio, responde por nota de voz e qualifica o lead com score de 0 a 100, com painel do operador em tempo real. As decisões de arquitetura estão em ADRs, com o trade-off de cada uma. | TypeScript · Node 20 · Express · Prisma · Socket.io · React · Docker |
| **SmartPalace** (privado) | PMS hoteleiro multi-tenant em produção, de autoria própria. 17 domínios, assistente de IA em port e adapter com provider falso determinístico para teste, dois gateways de pagamento atrás do mesmo contrato, 1.296 casos de teste. | Laravel · Livewire · PostgreSQL · Octane · Pest 4 |

Os repositórios públicos são o código mais recente que posso mostrar sem tocar em propriedade de empregador ou de cliente.

---

## Stack

**Principal:** PHP · Laravel · PostgreSQL · MySQL · React · TypeScript · Node.js · Docker

**Também trabalho com:** Angular · NestJS · Prisma · Inertia · Livewire · Tailwind · RabbitMQ · Redis

**Acompanho e uso com critério:** Go · Java · integração com LLM (structured output, STT e TTS)

---

## Contato

**[linkedin.com/in/erick-mendelski](https://www.linkedin.com/in/erick-mendelski/)**

Aberto a conversas sobre liderança técnica e arquitetura em produtos financeiros, e a projetos de recuperação de legado PHP/Laravel, migração de dados e auditoria de performance.
