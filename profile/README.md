# KURA × Clyvo Vet

**Plataforma veterinária em que a triagem por IA no WhatsApp do tutor, o prontuário do veterinário
e o financeiro do gestor são o mesmo dado.** Três aplicações, duas APIs e um serviço de IA sobre um
banco Oracle compartilhado.

Desenvolvido como **Challenge FIAP 2026** (2TDS), em parceria com a **Clyvo Vet**.

![FIAP Challenge 2026](https://img.shields.io/badge/FIAP-Challenge_2026-4A6944?style=flat-square)
![.NET 10](https://img.shields.io/badge/.NET-10-512BD4?style=flat-square&logo=dotnet&logoColor=white)
![Java 21](https://img.shields.io/badge/Java-21-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.2.5-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Python](https://img.shields.io/badge/Python-FastAPI-3776AB?style=flat-square&logo=python&logoColor=white)
![React Native](https://img.shields.io/badge/React_Native-0.81-61DAFB?style=flat-square&logo=react&logoColor=black)
![Oracle](https://img.shields.io/badge/Oracle-19c-F80000?style=flat-square&logo=oracle&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker&logoColor=white)

---

## Ver funcionando

| Demonstração | O que aparece |
|---|---|
| [**App da clínica**](https://youtube.com/shorts/Ik28Muwtljc) | Agenda, ficha do paciente, prontuário, receituário, teleconsulta, financeiro e o painel de triagens |
| [**App do tutor**](https://youtu.be/F62_LPbJORQ) | Pets, agendamento, vacinas vencendo, notificações e os consentimentos LGPD |

O ambiente inteiro sobe com um comando, em [`DevOps-Cloud`](https://github.com/KURA-Clyvo/DevOps-Cloud):
`docker compose up -d` levanta Oracle XE, as duas APIs e a Luna, com o schema criado do zero pelo
Flyway.

---

## A cadeia, na ordem em que acontece

O dado é digitado **uma vez**, no primeiro passo. Os quatro seguintes o reaproveitam.

| | Passo | Onde acontece |
|---|---|---|
| **1** | O tutor manda mensagem no WhatsApp. A Luna o identifica pelo telefone e recupera a clínica e os pets. | `kura-luna-ai` |
| **2** | A Luna classifica a urgência em ALTA, MÉDIA ou BAIXA e responde na hora. A triagem é registrada e chega ao painel da clínica. | `kura-luna-ai` → `backend-clinica-dotnet` |
| **3** | O veterinário atende: prontuário, receituário em PDF, teleconsulta. O áudio da consulta vira rascunho SOAP — que só entra no prontuário se ele confirmar. | `mobile-clinica-rn` |
| **4** | A cobrança nasce como **subrecurso do atendimento**, não como formulário à parte. O gestor vê receita, ticket médio e mix por serviço sem ninguém redigitar. | `backend-clinica-dotnet` |
| **5** | Histórico do pet, vacinas vencendo e notificações aparecem no app do tutor. | `backend-tutor-java` → `mobile-tutor-rn` |

O passo 4 é a decisão de produto de que mais nos orgulhamos: *o dado do gestor é subproduto do
fluxo do veterinário, nunca trabalho extra para ele.*

---

## Estado do projeto

Este é um projeto acadêmico com software que roda de verdade. Esta seção existe para que ninguém
precise adivinhar onde está a fronteira.

**Funciona, e dá para conferir no código:**

- Dois perfis de usuário separados **no servidor**, não na interface: um token de veterinário
  recebe `403` nas rotas financeiras, e isso está travado em teste automatizado.
- Prontuário atômico (consulta, vacina, exame e prescrição gravados junto do evento clínico numa
  transação única), receituário em PDF gerado no servidor, transcrição de áudio para rascunho SOAP,
  teleconsulta com sala de vídeo bloqueada quando falta o consentimento do tutor.
- Financeiro do período — receita bruta, ticket médio, mix por serviço e comparação com o período
  anterior — calculado numa leitura só, para os quatro números nunca discordarem entre si.
- Consentimento LGPD do tutor com registro insert-only, `Idempotency-Key` obrigatório, revogação,
  histórico e relatório de dados pessoais do titular (art. 18, I).
- Multi-tenancy por clínica no ORM, com um teste que quebra se uma entidade nova ficar de fora do
  filtro.
- Triagem por regras versionada, monitoramento de câmara fria com ESP32 e alerta de temperatura.

**É entrega acadêmica, não produto:** os blocos PL/SQL de
[`Mastering-Relational-Database`](https://github.com/KURA-Clyvo/Mastering-Relational-Database) e a
simulação de hardware no Wokwi em [`IOT-IA`](https://github.com/KURA-Clyvo/IOT-IA).

**Não existe, e não vamos dizer que existe:**

- **Nenhum cliente pagante e nenhuma venda.** Não há CAC, churn, MRR nem NPS medidos — só
  benchmark de mercado.
- **Os aplicativos nunca foram publicados em loja.** Não há avaliação de App Store ou Play Store.
- **Pagamentos, controle de estoque e plano de saúde pet** são roadmap desenhado, não construído.
- **Nenhuma certificação regulatória.** O receituário em PDF **não** tem assinatura ICP-Brasil, e
  não há controle de medicamento controlado. A Resolução CFMV 1.465/2022 e a RDC ANVISA 197/2017
  aparecem no código como **regra de negócio implementada**, o que é coisa diferente de
  certificação obtida.
- **Sensor IoT em campo.** O caminho de ingestão e alerta existe e é testado; o hardware está em
  simulação, não instalado numa clínica.

---

## Arquitetura

```
                 mobile-tutor-rn                mobile-clinica-rn
                 React Native · Expo            React Native · Expo
                 tutor                          veterinário + gestor
                        │                               │
                        │ REST                          │ REST
                        ▼                               ▼
              backend-tutor-java              backend-clinica-dotnet
              Java 21 · Spring Boot 3.2       .NET 10 · Clean Architecture
              :8081  contexto B2C             :8080  contexto B2B
                        │                               │  ▲
                        │                               │  │ X-Api-Key
                        │                               │  │
                        └──────────┬────────────────────┘  │
                                   ▼                       │
                        Oracle 19c (schema único)     kura-luna-ai
                        Flyway é a única autoridade   Python · FastAPI
                        de DDL · V1 → V19             :8000  WhatsApp/IA
                                                            │
                                                       Twilio (sandbox)
```

**As duas APIs não conversam por HTTP.** A integração é exclusivamente pelo schema Oracle
compartilhado, com propriedade de tabela declarada por contexto e um interceptor que lança exceção
em runtime se um lado tentar escrever na tabela do outro. A tabela `AGENDAMENTO` é a única
compartilhada para escrita, com trava otimista por versão — conflito devolve `409`.

Infraestrutura: **Docker Compose** para o ambiente completo e **Azure** para publicação. Não há
Kubernetes nem Terraform neste projeto.

---

## Repositórios

### Aplicação

| Repositório | O que é | Stack |
|---|---|---|
| [`backend-clinica-dotnet`](https://github.com/KURA-Clyvo/backend-clinica-dotnet) | API do lado clínico: prontuário, agenda, financeiro, tabela de preços, usuários da clínica, teleconsulta, IoT e os endpoints que a Luna consome. Health checks e OpenTelemetry. | .NET 10 · EF Core · Oracle · xUnit |
| [`backend-tutor-java`](https://github.com/KURA-Clyvo/backend-tutor-java) | API do tutor, com BFF próprio para o app e o módulo completo de consentimento LGPD. Flyway é a autoridade de DDL de todo o ecossistema. | Java 21 · Spring Boot 3.2.5 · Flyway · JUnit |
| [`kura-luna-ai`](https://github.com/KURA-Clyvo/kura-luna-ai) | Luna: triagem por regras, WhatsApp bidirecional via Twilio, lembrete de vacina e identificação de raça por foto. | Python · FastAPI · PyTorch · YOLOv8n |
| [`mobile-clinica-rn`](https://github.com/KURA-Clyvo/mobile-clinica-rn) | App da clínica — 12 telas, com os perfis de veterinário e de gestor separados. Roda na New Architecture do React Native. | React Native 0.81 · Expo 54 · TypeScript |
| [`mobile-tutor-rn`](https://github.com/KURA-Clyvo/mobile-tutor-rn) | App do tutor — 9 telas: pets, agenda, saúde, notificações e consentimentos. | React Native 0.81 · Expo 54 · TypeScript |

### Infraestrutura, dados e design

| Repositório | O que é | Stack |
|---|---|---|
| [`DevOps-Cloud`](https://github.com/KURA-Clyvo/DevOps-Cloud) | Compose do ambiente inteiro, pipelines de CI e o script que confere o contrato entre os apps e as APIs contra o Oracle real. | Docker Compose · GitHub Actions · Azure |
| [`IOT-IA`](https://github.com/KURA-Clyvo/IOT-IA) | Monitoramento de câmara fria de vacinas: ESP32 com DHT22 e LDR publicando por MQTT, Node-RED persistindo leitura e alerta, dashboard e correlação com clima externo. Faixa de 2 °C a 8 °C conforme a RDC ANVISA 197/2017. | ESP32 · MQTT · Node-RED · Wokwi |
| [`Mastering-Relational-Database`](https://github.com/KURA-Clyvo/Mastering-Relational-Database) | Modelagem e blocos PL/SQL sobre o schema do KURA — cursores, exceções e auditoria em `LOG_ERRO`. Entrega da disciplina. | Oracle · PL/SQL |
| [`design-system-docs-KURA`](https://github.com/KURA-Clyvo/design-system-docs-KURA) | Tokens e componentes das duas superfícies. `sage` é o contexto do tutor, `ocean` o da clínica — a mesma API de componente atende as duas sem bifurcar código. | HTML · CSS · TypeScript |
| [`Compliance-QA-Tests`](https://github.com/KURA-Clyvo/Compliance-QA-Tests) | Reservado para a disciplina de QA e compliance. **Ainda sem conteúdo.** | — |

---

## Números

Medidos em **setembro de 2026**, rodando os comandos nos repositórios. A contagem viva de cada
suíte está no CI do respectivo repositório.

| | |
|---|---|
| Telas de produto | 12 no app da clínica · 9 no app do tutor |
| Testes automatizados | **2.300** somados — .NET 672 · Java 197 · app clínica 1.077 · app tutor 172 · Luna 182 <sup>1</sup> |
| Banco compartilhado | 30 tabelas · migrations versionadas de V1 a V19 |
| Ambiente completo | 5 contêineres, do zero, por `docker compose up -d` |
| Integração contínua | ativa nos 6 repositórios de aplicação e infraestrutura |
| Triagem da Luna | 11 categorias de sintoma em 3 níveis · regras versão `1.0` |
| Identificação de raça | 37 rótulos · YOLOv8n para detecção, MobileNetV3-small para classificação <sup>2</sup> |

<sup>1</sup> A suíte completa da Luna exige Python 3.12 com `torch` e `ultralytics`; sem essas
dependências roda o subconjunto de 182 testes indicado acima.
<sup>2</sup> Os pesos treinados não são versionados neste repositório. Não publicamos métrica de
acurácia porque não mantemos um conjunto de avaliação com procedimento documentado — quando
houver, o número vem com a metodologia junto.

---

## Como a triagem funciona

A Luna **não** é um modelo generativo respondendo livremente. Ela compara a mensagem do tutor com
listas versionadas de sintomas, soma pontos por nível e devolve **quais palavras** dispararam a
classificação, junto da versão das regras que estava valendo.

| Nível | Categorias | Peso |
|---|---|---|
| `ALTA` | convulsão · sangramento · envenenamento · dispneia · trauma | 10 |
| `MEDIA` | vômito · diarreia · letargia · febre | 3 |
| `BAIXA` | dúvida de rotina · comportamento | 1 |

É por isso que chamamos a triagem de auditável: dá para explicar por que um caso subiu na fila, e
dá para versionar a mudança quando um veterinário discordar dela. **A IA sugere, o veterinário
decide** — nada entra no prontuário sem confirmação humana, que é o que a Resolução CFMV 1.465/2022
exige.

---

## Time

Turma 2TDS · Challenge FIAP 2026.

| Integrante | RM | Responsabilidade |
|---|---|---|
| [**Felipe Ferrete**](https://github.com/FelipeFerrete) | RM562999 | Tech lead · Backend .NET · IoT e IA |
| **Nikolas Brisola** | RM564371 | Backend Java · API do tutor |
| **Guilherme Sola** | RM563674 | Mobile tutor · UX |
| **Gustavo Bosak** | RM566315 | Mobile clínica · QA |
| **Clayton Alves** | RM562285 | DevOps · Banco de dados Oracle |

Para falar com a equipe, use o perfil de GitHub de cada integrante ou abra uma *issue* no
repositório correspondente.

---

## Contribuindo

Commits seguem [Conventional Commits](https://www.conventionalcommits.org/) em inglês; código e
comentários em português. Antes de abrir um PR, rode a suíte e o *linter* do repositório que você
tocou — os dois rodam no CI e barram o merge.

## Licença

Apenas [`design-system-docs-KURA`](https://github.com/KURA-Clyvo/design-system-docs-KURA) declara
licença **MIT** hoje. Os demais repositórios ainda **não têm arquivo de licença** e, por padrão do
GitHub, estão sob todos os direitos reservados. Estamos revisando isso repositório a repositório —
até lá, entre em contato antes de reutilizar código.

---

**KURA — o cuidado registrado.**
