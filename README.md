# Erick Mendelski

Engenheiro de software líder na **Qa+**, onde arquiteto plataformas financeiras multi-tenant em Laravel, React e PostgreSQL. Antes disso: hub de pagamentos e order book cripto (Navi), checkout e coprodução (TheMembers), ERP e migração de 9 anos de histórico contábil com validação de paridade.

O que faço melhor: recuperar sistema legado sem parar o produto, e transformar decisão técnica em decisão de negócio escrita.

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

- Lidero a engenharia dos produtos do grupo Qa+: defino stack, arquitetura e prioridade técnica, e respondo por disponibilidade, performance e custo de nuvem em produção.
- - Infraestrutura híbrida: VMs em datacenter nacional para o legado e Laravel Cloud para os produtos novos.
  - - Domínio recorrente: sistemas financeiros multi-tenant, integração de PDV e ERP, checkout, conciliação e migração de dados contábeis.
   
    - ---

    ## Três decisões técnicas, com o trade-off que aceitei

    As linhas abaixo apontam para o commit, não para a branch, então o link continua válido depois de qualquer refatoração.

    **1. O telefone do lead quando o WhatsApp entrega um LID em vez do número**

    Em contas com privacidade aumentada o remoteJid chega como LID (identificador interno) e, no Baileys novo, o LID às vezes vem disfarçado dentro de @s.whatsapp.net. Gravar isso como telefone contamina o CRM com número que não existe.

    Decidi resolver por cadeia de candidatos, senderPn → participantPn → remoteJidAlt → remoteJid, aceitando só o primeiro que passa numa validação de formato (BR: 12 ou 13 dígitos; demais DDIs: 10 a 13).

    **Trade-off:** E.164 vai até 15 dígitos, e cortar em 13 descarta um caso teórico raríssimo para barrar praticamente todo LID disfarçado. Preferi lead sem telefone, editável no painel, a lead com telefone falso.

    → [whatsapp/utils.ts#L21-L56](https://github.com/Mendelski/ai-chatbot/blob/431f90a41cab8d2b13266a903b40bffe6efb8b42/backend/src/modules/whatsapp/utils.ts#L21-L56) · [whatsapp/handler.ts#L49-L55](https://github.com/Mendelski/ai-chatbot/blob/431f90a41cab8d2b13266a903b40bffe6efb8b42/backend/src/modules/whatsapp/handler.ts#L49-L55)

    **2. O pushName do WhatsApp não vira nome do lead**

    O caminho fácil é gravar o pushName como nome do contato. Na prática ele é apelido de exibição: emoji, iniciais, "Vendas 2".

    Decidi que a baseline do lead grava **apenas** o telefone. O nome só entra quando o usuário confirma na conversa. O pushName vai para o prompt explicitamente rotulado como baixa fidelidade, para servir de dica social sem virar dado.

    **Trade-off:** o lead nasce sem nome e a IA gasta uma pergunta. Aceitei: nome errado no CRM é caro de descobrir e estraga a abordagem comercial.

    → [lead/service.ts#L24-L38](https://github.com/Mendelski/ai-chatbot/blob/431f90a41cab8d2b13266a903b40bffe6efb8b42/backend/src/modules/lead/service.ts#L24-L38)

    **3. Uma chamada de IA por mensagem, com saída tipada**

    O padrão comum é encadear chamadas: transcrever, responder, classificar intenção, extrair lead. São 3 ou 4 round-trips por mensagem, com latência somada e custo multiplicado.

    Decidi uma única chamada multimodal com responseSchema declarado (reply, intent como enum, qualified, lead_score, lead_data, send_audio, transcription, reaction), com o áudio inline no mesmo request.

    **Trade-off:** tudo depende de um JSON. Se ele vier malformado, perco a mensagem inteira. Mitiguei com parser defensivo e resposta de fallback, clamp de score em 0-100, enum de intent revalidado no servidor e reação normalizada para um único grapheme. Coberto por testes.

    → [ai/schema.ts#L3-L42](https://github.com/Mendelski/ai-chatbot/blob/431f90a41cab8d2b13266a903b40bffe6efb8b42/backend/src/modules/ai/schema.ts#L3-L42) · [ai/service.ts#L47-L90](https://github.com/Mendelski/ai-chatbot/blob/431f90a41cab8d2b13266a903b40bffe6efb8b42/backend/src/modules/ai/service.ts#L47-L90)

    ---

    ## Projetos em destaque

    | Projeto | O que é | Stack |
    |---|---|---|
    | **[ai-chatbot](https://github.com/Mendelski/ai-chatbot)** | Bot de WhatsApp com Gemini multimodal: transcreve áudio, responde por nota de voz e qualifica o lead com score 0-100, com painel do operador em tempo real. 4 ADRs escritos. | TypeScript · Node 20 · Express · Prisma/SQLite · Socket.io · React · Docker |
    | **[todolist-api-laravel12](https://github.com/Mendelski/todolist-api-laravel12)** | API REST de tarefas com JWT, Policies por dono, versionamento /api/v1, organização por domínio e activity log em MongoDB. 41 casos de teste em Pest 4. | Laravel 12 · PHP 8.2+ · MySQL · MongoDB · Pest 4 |
    | **[news-manager-laravel12](https://github.com/Mendelski/news-manager-laravel12)** | Gestão de notícias full-stack num único deploy: Inertia 2 + React 19, autenticação Fortify com 2FA, lint e typecheck no CI. | Laravel 12 · React 19 · Inertia 2 · Tailwind 4 · Pest 4 |

    Os três são resoluções de desafios técnicos, mantidas públicas de propósito: é o código mais recente que posso mostrar sem tocar em propriedade de empregador.

    ---

    ## Stack

    **Principal:** PHP · Laravel · PostgreSQL · MySQL · React · TypeScript · Node.js · Docker

    **Também trabalho com:** Angular · NestJS · Prisma · Inertia · Tailwind · RabbitMQ · Redis

    **Acompanho e uso com critério:** Go · Java · integração com LLM (Gemini, structured output, STT/TTS)

    ---

    ## Contato

    - LinkedIn: **[linkedin.com/in/erick-mendelski](https://www.linkedin.com/in/erick-mendelski/)**
   
    - Aberto a conversas sobre liderança técnica e arquitetura em produtos financeiros, e a projetos de recuperação de legado PHP/Laravel, migração de dados e auditoria de performance.
    - 
