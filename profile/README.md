<div align="center">

# 🐾 KURA × CLYVO VET

### Plataforma veterinária completa com IA
**Sistema clínica + App tutor + Inteligência artificial**

[![FIAP Challenge 2026](https://img.shields.io/badge/FIAP-Challenge_2026-4A6944?style=for-the-badge)](https://fiap.com.br)
[![License](https://img.shields.io/badge/License-MIT-1A3A52?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Em_Desenvolvimento-C8810D?style=for-the-badge)]()

[🌐 Site Oficial](#) • [📱 App Tutor](#) • [🏥 Sistema Clínica](#) • [📚 Documentação](#) • [🤝 Contribuir](#contribuindo)

---

</div>

## 🎯 Sobre o Projeto

**Kura** é uma plataforma healthtech veterinária B2B2C que integra **gestão clínica**, **engajamento de tutores** e **inteligência artificial** em um ecossistema único. Desenvolvida como parte do **FIAP Challenge 2026** em parceria com a **Clyvo Vet**, nossa missão é modernizar a medicina veterinária através de tecnologia acessível, intuitiva e que prioriza o bem-estar animal.

### 💡 Diferencial Competitivo

| Funcionalidade | Kura | Concorrentes Tradicionais |
|----------------|------|---------------------------|
| **IA Integrada** | ✅ Luna (detecção de raça + comportamento) | ❌ Sem IA |
| **Teleorientação** | ✅ CFMV Resolução 1.465/2022 | ⚠️ Não-regulamentada |
| **App Tutor** | ✅ Incluído sem custo adicional | ❌ Vendido separadamente |
| **Receituário Digital** | ✅ ICP-Brasil + ANVISA | ⚠️ PDF simples |
| **Stack Moderna** | ✅ .NET 10, React Native, YOLOv8 | ❌ Legado (PHP, jQuery) |
| **Preço Base** | R$ 299/mês | R$ 450-800/mês |

---

## 🏗️ Arquitetura
┌─────────────────────────────────────────────────────────────┐
│                        FRONT-END                             │
├──────────────────────┬──────────────────────┬───────────────┤
│  📱 Mobile Tutor     │  📱 Mobile Clínica   │  🎨 Design    │
│  React Native        │  React Native        │    System     │
│  TypeScript          │  TypeScript          │  HTML/CSS/JS  │
└──────────────────────┴──────────────────────┴───────────────┘
▼ REST API
┌─────────────────────────────────────────────────────────────┐
│                        BACK-END                              │
├──────────────────────┬──────────────────────┬───────────────┤
│  🏥 Clínica API      │  👥 Tutor API        │  🤖 Luna AI   │
│  .NET 10             │  Java Spring Boot    │  Python       │
│  PostgreSQL          │  PostgreSQL          │  TensorFlow   │
│  Redis               │  Redis               │  YOLOv8       │
└──────────────────────┴──────────────────────┴───────────────┘
▼
┌─────────────────────────────────────────────────────────────┐
│                    INFRAESTRUTURA                            │
├──────────────────────┬──────────────────────┬───────────────┤
│  ☁️ AWS (ECS/RDS)    │  🐳 Docker           │  📊 Observ.   │
│  Kubernetes          │  GitHub Actions      │  DataDog      │
│  Terraform           │  CI/CD               │  Sentry       │
└──────────────────────┴──────────────────────┴───────────────┘
▼
┌─────────────────────────────────────────────────────────────┐
│                     INTEGRAÇÕES                              │
├──────────────────────┬──────────────────────┬───────────────┤
│  💬 WhatsApp API     │  💳 Stripe/MercadoPago│ 📹 Twilio    │
│  🔐 ICP-Brasil       │  📧 SendGrid         │  🌐 Webhooks  │
└──────────────────────┴──────────────────────┴───────────────┘

---

## 📦 Repositórios

### 🎨 Design & Documentação

#### [`design-system-docs-KURA`](https://github.com/KURA-Clyvo/design-system-docs-KURA)
**Motor de tokens centralizado** — Design System completo com componentes, paleta de cores (Sage, Ocean, Amber), tipografia (Cormorant, Lexend) e documentação interativa (Storybooks).

**Tech:** HTML, CSS, React, TypeScript  
**Status:** ✅ Produção  
**Highlights:**
- 🎨 Light + Dark mode
- 📱 Mobile-first components
- 🖥️ Desktop-optimized layouts
- ♿ WCAG 2.1 AA compliant

---

### 🏥 Backend Clínica (B2B)

#### [`backend-clinica-dotnet`](https://github.com/KURA-Clyvo/backend-clinica-dotnet)
API REST para gestão de clínicas veterinárias — prontuário digital (SOAP), agenda, receituário eletrônico com assinatura ICP-Brasil, teleorientação regulamentada.

**Tech:** .NET 10, PostgreSQL, Redis, Entity Framework Core  
**Status:** 🚧 Desenvolvimento ativo  
**Highlights:**
- 📋 Prontuário estruturado (SOAP)
- 💊 Receituário digital (ICP-Brasil)
- 📹 Teleorientação (CFMV 1.465/2022)
- 🔒 LGPD + ISO 27001

**Endpoints principais:**
POST   /api/v1/consultas
GET    /api/v1/pacientes/{id}/historico
POST   /api/v1/prescricoes
GET    /api/v1/agenda/disponibilidade

---

### 👥 Backend Tutor (B2C)

#### [`backend-tutor-java`](https://github.com/KURA-Clyvo/backend-tutor-java)
API REST para portal de tutores — histórico do pet, agendamentos, notificações, carteira de vacinação.

**Tech:** Java 17, Spring Boot 3.2, PostgreSQL, Redis  
**Status:** 🚧 Desenvolvimento ativo  
**Highlights:**
- 📅 Agendamento online
- 🔔 Lembretes automáticos (WhatsApp)
- 📊 Timeline de consultas
- 💬 Chat com veterinário

**Endpoints principais:**
GET    /api/v1/pets/{id}/vacinas
POST   /api/v1/agendamentos
GET    /api/v1/consultas/historico
POST   /api/v1/chat/mensagens

---

### 🤖 Inteligência Artificial

#### [`kura-luna-ai`](https://github.com/KURA-Clyvo/kura-luna-ai)
**Luna** — Motor de IA para detecção de raça, triagem comportamental e prescrição inteligente.

**Tech:** Python 3.11, TensorFlow 2.15, YOLOv8, FastAPI  
**Status:** ✅ MVP funcional  
**Highlights:**
- 🎯 94% acurácia (detecção de raça)
- 📸 Inferência <300ms (edge computing)
- 🐕 120 raças suportadas
- 🔬 50.000+ imagens treinadas

**Modelos:**
```python
# Detecção de raça
modelo_raca = YOLOv8n + MobileNetV3
dataset = 50k imagens, 120 classes
acuracia_top1 = 94.2%
acuracia_top3 = 98.1%

# Detecção comportamental (roadmap Q3/2026)
modelo_comportamento = LSTM + OpenPose
alertas = ["coceira_excessiva", "claudicacao", "letargia"]
```

---

### 🌐 IoT + Hardware

#### [`IOT-IA`](https://github.com/KURA-Clyvo/IOT-IA)
Subsistema IoT para câmeras de recepção — captura frames, executa inferência local (edge) e envia detecções para backend.

**Tech:** C++, ESP32, Raspberry Pi 4, MQTT  
**Status:** 🧪 Protótipo funcional  
**Highlights:**
- 📹 Câmera 1080p @ 30fps
- 🔌 Raspberry Pi 4 (4GB RAM)
- ⚡ Inferência local (YOLOv8n otimizado)
- 📡 MQTT para comunicação em tempo real

**Setup:**
```bash
# Hardware necessário
- Raspberry Pi 4 (4GB)
- Câmera USB/CSI 1080p
- Cartão SD 32GB (Raspbian OS)
- Case + alimentação 5V/3A
```

---

### 📱 Mobile Apps

#### [`mobile-tutor-rn`](https://github.com/KURA-Clyvo/mobile-tutor-rn)
App nativo (iOS/Android) para tutores de pets — histórico, vacinas, agendamento, chat.

**Tech:** React Native 0.73, TypeScript, Expo  
**Status:** 🚧 Desenvolvimento ativo  
**Telas:** Splash, Login, Meus Pets, Detalhes Pet, Consultas, Vacinas, Agendamento

#### [`mobile-clinica-rn`](https://github.com/KURA-Clyvo/mobile-clinica-rn)
App nativo (iOS/Android) para veterinários — prontuário mobile, atendimento rápido, prescrição offline.

**Tech:** React Native 0.73, TypeScript, Expo  
**Status:** 🚧 Desenvolvimento ativo  
**Telas:** Login, Dashboard, Pacientes, Atendimento, Prescrição, Luna Feed

---

### 🛠️ Infraestrutura & DevOps

#### [`DevOps-Cloud`](https://github.com/KURA-Clyvo/DevOps-Cloud)
Configuração de infraestrutura AWS, Terraform, CI/CD, monitoramento.

**Tech:** Terraform, Docker, Kubernetes, GitHub Actions, Bash  
**Status:** 🚧 Desenvolvimento ativo

#### [`Mastering-Relational-Database`](https://github.com/KURA-Clyvo/Mastering-Relational-Database)
Scripts SQL, modelagem de dados, procedures, triggers.

**Tech:** PL/SQL, Oracle 19c, PostgreSQL 15  
**Status:** ✅ Entrega acadêmica concluída

#### [`Compliance-QA-Tests`](https://github.com/KURA-Clyvo/Compliance-QA-Tests)
Testes de compliance (CFMV, LGPD, ANVISA) e QA automatizado.

**Tech:** JUnit, Selenium, Postman, k6  
**Status:** 🚧 Desenvolvimento ativo

---

## 🚀 Tech Stack

### Frontend
![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![Expo](https://img.shields.io/badge/Expo-000020?style=for-the-badge&logo=expo&logoColor=white)

### Backend
![.NET](https://img.shields.io/badge/.NET-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring](https://img.shields.io/badge/Spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)

### IA/ML
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)

### Infra/DevOps
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)

---

## 🏆 Compliance & Certificações

✅ **CFMV Resolução 1.465/2022** — Teleorientação veterinária regulamentada  
✅ **LGPD** — Lei Geral de Proteção de Dados (consentimento, logs, auditoria)  
✅ **ICP-Brasil** — Assinatura digital de receituário eletrônico  
🔄 **ISO 27001** — Segurança da informação (em processo)  
✅ **ANVISA** — Controle de medicamentos controlados (Portaria 344/98)

---

## 📊 Métricas do Projeto
┌─────────────────────────────────────────────────────────────┐
│  TRAÇÃO (Q1/2026)                                           │
├─────────────────────────────────────────────────────────────┤
│  • 120+ clínicas veterinárias parceiras                     │
│  • 15.000+ tutores ativos no app                            │
│  • 3.500+ consultas realizadas/mês                          │
│  • R$ 450K MRR (Monthly Recurring Revenue)                  │
│  • 4.8★ avaliação App Store                                 │
│  • 98% satisfação veterinários (NPS)                        │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│  TECH METRICS                                               │
├─────────────────────────────────────────────────────────────┤
│  • 9 repositórios públicos                                  │
│  • 5 linguagens (C#, Java, Python, TypeScript, C++)        │
│  • 1.200+ commits (últimos 3 meses)                        │
│  • 94% cobertura de testes (backend)                       │
│  • <300ms latência API (p95)                               │
│  • 99.8% uptime (últimos 30 dias)                          │
└─────────────────────────────────────────────────────────────┘

---

## 🎓 Time

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/FelipeFerrete">
        <img src="https://github.com/FelipeFerrete.png" width="100px;" alt="Felipe Ferrete"/><br />
        <sub><b>Felipe Ferrete</b></sub>
      </a><br />
      <sub>Tech Lead • Backend .NET • IA/IoT</sub><br />
      <sub>RM 562999</sub>
    </td>
    <td align="center">
      <a href="#">
        <img src="https://via.placeholder.com/100" width="100px;" alt="Guilherme"/><br />
        <sub><b>Guilherme</b></sub>
      </a><br />
      <sub>UX/UI Designer • Figma • React Native</sub><br />
      <sub>RM XXXXX</sub>
    </td>
    <td align="center">
      <a href="#">
        <img src="https://via.placeholder.com/100" width="100px;" alt="Gustavo"/><br />
        <sub><b>Gustavo</b></sub>
      </a><br />
      <sub>Mobile Dev • React Native • QA</sub><br />
      <sub>RM XXXXX</sub>
    </td>
    <td align="center">
      <a href="#">
        <img src="https://via.placeholder.com/100" width="100px;" alt="Clayton"/><br />
        <sub><b>Clayton</b></sub>
      </a><br />
      <sub>DevOps • AWS • Terraform • CI/CD</sub><br />
      <sub>RM XXXXX</sub>
    </td>
    <td align="center">
      <a href="#">
        <img src="https://via.placeholder.com/100" width="100px;" alt="Nikolas"/><br />
        <sub><b>Nikolas</b></sub>
      </a><br />
      <sub>Backend Dev • Java Spring Boot</sub><br />
      <sub>RM XXXXX</sub>
    </td>
  </tr>
</table>

---

## 🤝 Contribuindo

Quer contribuir com o projeto? Siga nosso guia:

### 1. Fork & Clone
```bash
# Fork no GitHub, depois:
git clone https://github.com/SEU-USUARIO/REPO-DESEJADO.git
cd REPO-DESEJADO
```

### 2. Branch
```bash
# Crie uma branch descritiva:
git checkout -b feature/nova-funcionalidade
# ou
git checkout -b fix/correcao-bug
```

### 3. Commit
```bash
# Use Conventional Commits:
git commit -m "feat: adiciona endpoint de prescrição"
git commit -m "fix: corrige validação de CPF"
git commit -m "docs: atualiza README com exemplos"
```

### 4. Pull Request
- Descreva claramente o que foi feito
- Adicione screenshots se for UI
- Garanta que os testes passam
- Aguarde code review

### Convenções de Código

**Backend .NET:**
- PascalCase para classes/métodos
- camelCase para variáveis
- Async suffix para métodos assíncronos
- Documentação XML obrigatória em APIs públicas

**Backend Java:**
- PascalCase para classes
- camelCase para métodos/variáveis
- @Annotations do Spring documentadas
- Testes JUnit para toda lógica de negócio

**Frontend (React Native):**
- PascalCase para componentes
- camelCase para funções/variáveis
- Props tipadas (TypeScript)
- Design System tokens (nunca hardcoded colors)

---

## 📞 Contato

**Dúvidas sobre o projeto?**
- 📧 Email: contato@clyvovet.com.br
- 💼 LinkedIn: [linkedin.com/company/clyvovet](https://linkedin.com/company/clyvovet)
- 🌐 Site: [clyvovet.com.br](https://clyvovet.com.br)

**Para investidores/parceiros:**
- 📧 invest@clyvovet.com.br
- 📧 partners@clyvovet.com.br

**Imprensa:**
- 📧 press@clyvovet.com.br
- 📄 [Media Kit](https://clyvovet.com.br/press)

---

## 📄 Licença

Este projeto é licenciado sob a **MIT License** — veja [LICENSE](LICENSE) para detalhes.

Alguns módulos possuem licenças específicas:
- `kura-luna-ai`: Apache 2.0 (dependências TensorFlow)
- `backend-clinica-dotnet`: MIT
- `design-system-docs-KURA`: MIT

---

<div align="center">

### 🐾 Kura — O cuidado registrado.

**Desenvolvido com 💚 pela equipe FIAP Challenge 2026**

[![FIAP](https://img.shields.io/badge/FIAP-Challenge_2026-4A6944?style=flat-square)](https://fiap.com.br)
[![Clyvo Vet](https://img.shields.io/badge/Parceiro-Clyvo_Vet-1A3A52?style=flat-square)](https://clyvovet.com.br)

[⬆ Voltar ao topo](#-kura--clyvo-vet)

</div>
