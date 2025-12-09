# Plataforma Taty - Documentação para Apresentação

## Visão Geral do Sistema

**Nome do Projeto:** Plataforma Taty
**Tipo:** Plataforma de Ensino Online (EAD)
**Domínio:** Cursos de Harmonização Facial para profissionais da saúde
**Tecnologias:** Next.js 15, React 19, PostgreSQL, Stripe, Bunny Stream

---

# 1. REQUISITOS DE USUÁRIO

## 1.1 Requisitos Funcionais do Usuário (Aluno)

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RU01 | O usuário deve poder criar uma conta com nome, email e senha | Alta |
| RU02 | O usuário deve poder fazer login com email e senha | Alta |
| RU03 | O usuário deve poder recuperar sua senha via email | Alta |
| RU04 | O usuário deve poder visualizar os cursos disponíveis | Alta |
| RU05 | O usuário deve poder comprar um curso via cartão de crédito | Alta |
| RU06 | O usuário deve poder assistir às aulas dos cursos adquiridos | Alta |
| RU07 | O usuário deve poder acompanhar seu progresso no curso | Média |
| RU08 | O usuário deve poder gerar certificado ao completar o curso | Média |
| RU09 | O usuário deve poder gerenciar seu perfil e dados pessoais | Média |
| RU10 | O usuário deve poder cadastrar múltiplos endereços de entrega | Média |
| RU11 | O usuário deve poder visualizar histórico de pedidos | Baixa |
| RU12 | O usuário deve poder rastrear entregas de produtos físicos | Média |
| RU13 | O usuário deve poder configurar preferências de notificação | Baixa |

## 1.2 Requisitos Funcionais do Usuário (Administrador)

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RA01 | O admin deve poder criar, editar e excluir cursos | Alta |
| RA02 | O admin deve poder gerenciar módulos e aulas de cada curso | Alta |
| RA03 | O admin deve poder fazer upload de vídeos para as aulas | Alta |
| RA04 | O admin deve poder visualizar lista de alunos e seus progressos | Alta |
| RA05 | O admin deve poder gerenciar pedidos e status de envio | Alta |
| RA06 | O admin deve poder atualizar códigos de rastreamento | Média |
| RA07 | O admin deve poder ativar/desativar contas de usuários | Média |
| RA08 | O admin deve poder visualizar estatísticas e relatórios | Média |
| RA09 | O admin deve poder testar envio de emails | Baixa |
| RA10 | O admin deve poder agendar publicação de aulas | Média |

## 1.3 Requisitos Não-Funcionais do Usuário

| ID | Requisito | Categoria |
|----|-----------|-----------|
| RNF-U01 | A interface deve ser em português brasileiro | Usabilidade |
| RNF-U02 | O sistema deve ser acessível em dispositivos móveis | Usabilidade |
| RNF-U03 | Os vídeos devem carregar em menos de 5 segundos | Desempenho |
| RNF-U04 | O processo de compra deve ser concluído em no máximo 5 etapas | Usabilidade |

---

# 2. REQUISITOS DE SISTEMA

## 2.1 Requisitos Funcionais do Sistema

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RS01 | O sistema deve autenticar usuários via JWT com expiração de 30 dias | Alta |
| RS02 | O sistema deve criptografar senhas usando bcrypt com salt de 10 rounds | Alta |
| RS03 | O sistema deve validar força de senha (maiúscula, minúscula, número, especial, mín. 8 chars) | Alta |
| RS04 | O sistema deve processar pagamentos via Stripe (cartão de crédito) | Alta |
| RS05 | O sistema deve receber webhooks do Stripe para confirmar pagamentos | Alta |
| RS06 | O sistema deve criar matrícula automaticamente após pagamento confirmado | Alta |
| RS07 | O sistema deve enviar email de confirmação após compra | Alta |
| RS08 | O sistema deve hospedar e transmitir vídeos via Bunny Stream (HLS) | Alta |
| RS09 | O sistema deve rastrear progresso de aulas por usuário | Média |
| RS10 | O sistema deve gerar certificados em PDF no lado do cliente | Média |
| RS11 | O sistema deve implementar rate limiting (5 tentativas/15min) em login/registro | Alta |
| RS12 | O sistema deve cachear dados em Redis para otimização | Média |
| RS13 | O sistema deve integrar com Correios e Jadlog para rastreamento | Média |
| RS14 | O sistema deve enviar notificações por email (Resend) | Média |
| RS15 | O sistema deve processar jobs em background via Inngest | Baixa |
| RS16 | O sistema deve armazenar imagens no Supabase Storage | Média |
| RS17 | O sistema deve controlar acesso baseado em roles (STUDENT, ADMIN) | Alta |
| RS18 | O sistema deve expirar acesso de usuário após período configurado | Média |

## 2.2 Requisitos Não-Funcionais do Sistema

| ID | Requisito | Categoria | Especificação |
|----|-----------|-----------|---------------|
| RNF-S01 | Tempo de resposta da página inicial | Desempenho | < 1 segundo |
| RNF-S02 | Disponibilidade do sistema | Confiabilidade | 99.9% uptime |
| RNF-S03 | Suporte a usuários simultâneos | Escalabilidade | Mínimo 1000 usuários |
| RNF-S04 | Criptografia de dados em trânsito | Segurança | HTTPS/TLS 1.3 |
| RNF-S05 | Backup do banco de dados | Confiabilidade | Diário |
| RNF-S06 | Compatibilidade de navegadores | Portabilidade | Chrome, Firefox, Safari, Edge |
| RNF-S07 | Framework de desenvolvimento | Tecnologia | Next.js 15, React 19 |
| RNF-S08 | Banco de dados | Tecnologia | PostgreSQL |
| RNF-S09 | Hospedagem de vídeos | Tecnologia | Bunny Stream CDN |
| RNF-S10 | Processamento de pagamentos | Tecnologia | Stripe |
| RNF-S11 | Cache distribuído | Tecnologia | Upstash Redis |

---

# 3. DIAGRAMAS DE CASOS DE USO

## 3.1 Diagrama de Casos de Uso - Visão Geral

```mermaid
graph TB
    subgraph Sistema["Sistema Plataforma Taty"]
        UC1["Cadastrar-se"]
        UC2["Fazer Login"]
        UC3["Recuperar Senha"]
        UC4["Visualizar Cursos"]
        UC5["Comprar Curso"]
        UC6["Assistir Aulas"]
        UC7["Acompanhar Progresso"]
        UC8["Gerar Certificado"]
        UC9["Gerenciar Perfil"]
        UC10["Gerenciar Endereços"]
        UC11["Ver Histórico de Pedidos"]
        UC12["Rastrear Entregas"]

        UC20["Gerenciar Cursos"]
        UC21["Gerenciar Módulos/Aulas"]
        UC22["Upload de Vídeos"]
        UC23["Gerenciar Usuários"]
        UC24["Gerenciar Pedidos"]
        UC25["Ver Estatísticas"]
    end

    Aluno((Aluno))
    Admin((Administrador))
    Stripe[["Stripe"]]
    BunnyStream[["Bunny Stream"]]
    Correios[["Correios/Jadlog"]]

    Aluno --> UC1
    Aluno --> UC2
    Aluno --> UC3
    Aluno --> UC4
    Aluno --> UC5
    Aluno --> UC6
    Aluno --> UC7
    Aluno --> UC8
    Aluno --> UC9
    Aluno --> UC10
    Aluno --> UC11
    Aluno --> UC12

    Admin --> UC20
    Admin --> UC21
    Admin --> UC22
    Admin --> UC23
    Admin --> UC24
    Admin --> UC25

    UC5 -.->|<<usa>>| Stripe
    UC6 -.->|<<usa>>| BunnyStream
    UC22 -.->|<<usa>>| BunnyStream
    UC12 -.->|<<usa>>| Correios
    UC24 -.->|<<usa>>| Correios
```

## 3.2 Diagrama de Casos de Uso - Módulo de Autenticação

```mermaid
graph LR
    subgraph Autenticação
        UC1[Cadastrar-se]
        UC2[Fazer Login]
        UC3[Recuperar Senha]
        UC4[Validar Token]
        UC5[Redefinir Senha]
    end

    Usuario((Usuário))

    Usuario --> UC1
    Usuario --> UC2
    Usuario --> UC3
    UC3 -.->|<<inclui>>| UC4
    UC4 -.->|<<inclui>>| UC5
```

## 3.3 Diagrama de Casos de Uso - Módulo de Compras

```mermaid
graph TB
    subgraph Compras
        UC1[Visualizar Catálogo]
        UC2[Selecionar Curso]
        UC3[Adicionar Dados Pessoais]
        UC4[Informar Endereço]
        UC5[Realizar Pagamento]
        UC6[Confirmar Pedido]
        UC7[Criar Matrícula]
    end

    Aluno((Aluno))
    Stripe[["Stripe"]]
    Email[["Sistema de Email"]]

    Aluno --> UC1
    Aluno --> UC2
    UC2 -.->|<<inclui>>| UC3
    UC3 -.->|<<inclui>>| UC4
    UC4 -.->|<<inclui>>| UC5
    UC5 -.->|<<usa>>| Stripe
    UC5 -.->|<<inclui>>| UC6
    UC6 -.->|<<inclui>>| UC7
    UC6 -.->|<<usa>>| Email
```

## 3.4 Casos de Uso Detalhados

### UC01 - Cadastrar-se

| Campo | Descrição |
|-------|-----------|
| **Nome** | Cadastrar-se |
| **Ator Principal** | Usuário não autenticado |
| **Pré-condições** | Usuário não possui conta no sistema |
| **Pós-condições** | Conta criada e usuário logado automaticamente |
| **Fluxo Principal** | 1. Usuário acessa página de cadastro<br>2. Sistema exibe formulário<br>3. Usuário preenche nome, email e senha<br>4. Sistema valida dados e força da senha<br>5. Sistema cria conta com expiração de 1 ano<br>6. Sistema realiza login automático<br>7. Sistema redireciona para cursos |
| **Fluxo Alternativo** | 4a. Email já cadastrado → Sistema exibe erro<br>4b. Senha fraca → Sistema exibe requisitos |

### UC05 - Comprar Curso

| Campo | Descrição |
|-------|-----------|
| **Nome** | Comprar Curso |
| **Ator Principal** | Aluno |
| **Atores Secundários** | Stripe, Sistema de Email |
| **Pré-condições** | Curso disponível para venda |
| **Pós-condições** | Pagamento processado e matrícula criada |
| **Fluxo Principal** | 1. Aluno seleciona curso<br>2. Sistema exibe página de checkout<br>3. Aluno preenche dados pessoais (se não logado)<br>4. Aluno preenche endereço<br>5. Sistema cria sessão no Stripe<br>6. Aluno é redirecionado para Stripe Checkout<br>7. Aluno realiza pagamento<br>8. Stripe envia webhook de confirmação<br>9. Sistema atualiza status do pagamento<br>10. Sistema cria matrícula<br>11. Sistema envia email de confirmação |
| **Fluxo Alternativo** | 7a. Pagamento falha → Sistema registra falha<br>8a. Webhook não recebido → Pagamento fica pendente |

### UC06 - Assistir Aulas

| Campo | Descrição |
|-------|-----------|
| **Nome** | Assistir Aulas |
| **Ator Principal** | Aluno matriculado |
| **Atores Secundários** | Bunny Stream |
| **Pré-condições** | Aluno autenticado e matriculado no curso |
| **Pós-condições** | Progresso da aula registrado |
| **Fluxo Principal** | 1. Aluno acessa curso<br>2. Sistema verifica matrícula<br>3. Sistema exibe lista de módulos e aulas<br>4. Aluno seleciona aula<br>5. Sistema carrega vídeo do Bunny Stream<br>6. Aluno assiste aula<br>7. Aluno marca aula como concluída<br>8. Sistema registra progresso |
| **Fluxo Alternativo** | 2a. Sem matrícula → Sistema redireciona para compra<br>4a. Aula não publicada → Sistema oculta aula |

### UC08 - Gerar Certificado

| Campo | Descrição |
|-------|-----------|
| **Nome** | Gerar Certificado |
| **Ator Principal** | Aluno |
| **Pré-condições** | Aluno completou 100% das aulas do curso |
| **Pós-condições** | Certificado em PDF baixado |
| **Fluxo Principal** | 1. Aluno acessa área de certificados<br>2. Sistema verifica progresso = 100%<br>3. Sistema gera certificado com dados do aluno e curso<br>4. Sistema converte para PDF (html2canvas + jsPDF)<br>5. Sistema inicia download do certificado |
| **Fluxo Alternativo** | 2a. Progresso < 100% → Sistema exibe progresso atual |

---

# 4. DIAGRAMAS DE ATIVIDADE

## 4.1 Diagrama de Atividade - Processo de Compra de Curso

```mermaid
flowchart TD
    Start([Início]) --> A[Acessar página de compra]
    A --> B{Usuário logado?}

    B -->|Não| C[Exibir formulário de cadastro/login]
    C --> D[Preencher dados pessoais]
    D --> E[Validar dados]
    E --> F{Dados válidos?}
    F -->|Não| D
    F -->|Sim| G[Criar/autenticar usuário]

    B -->|Sim| H[Carregar dados do usuário]
    G --> H

    H --> I[Exibir formulário de endereço]
    I --> J[Preencher/selecionar endereço]
    J --> K[Validar endereço]
    K --> L{Endereço válido?}
    L -->|Não| J
    L -->|Sim| M[Criar registro de pagamento]

    M --> N[Criar sessão Stripe Checkout]
    N --> O[Redirecionar para Stripe]
    O --> P[Processar pagamento no Stripe]

    P --> Q{Pagamento aprovado?}
    Q -->|Não| R[Exibir erro de pagamento]
    R --> S{Tentar novamente?}
    S -->|Sim| O
    S -->|Não| End1([Fim - Cancelado])

    Q -->|Sim| T[Stripe envia webhook]
    T --> U[Atualizar status pagamento: SUCCEEDED]
    U --> V[Ativar conta do usuário]
    V --> W[Criar matrícula no curso]
    W --> X[Enviar email de confirmação]
    X --> Y[Redirecionar para área do curso]
    Y --> End2([Fim - Sucesso])
```

## 4.2 Diagrama de Atividade - Fluxo de Autenticação

```mermaid
flowchart TD
    Start([Início]) --> A[Acessar página de login]
    A --> B[Preencher email e senha]
    B --> C[Submeter formulário]

    C --> D{Rate limit atingido?}
    D -->|Sim| E[Exibir erro: muitas tentativas]
    E --> F[Aguardar 15 minutos]
    F --> B

    D -->|Não| G[Buscar usuário por email]
    G --> H{Usuário existe?}
    H -->|Não| I[Exibir erro: credenciais inválidas]
    I --> B

    H -->|Sim| J[Validar senha com bcrypt]
    J --> K{Senha correta?}
    K -->|Não| I

    K -->|Sim| L{Conta ativa?}
    L -->|Não| M[Exibir erro: conta desativada]
    M --> End1([Fim - Bloqueado])

    L -->|Sim| N{Conta expirada?}
    N -->|Sim| O[Exibir erro: conta expirada]
    O --> End2([Fim - Expirado])

    N -->|Não| P[Gerar token JWT]
    P --> Q[Criar sessão]
    Q --> R[Salvar em cookie HTTP-only]
    R --> S[Redirecionar para dashboard]
    S --> End3([Fim - Sucesso])
```

## 4.3 Diagrama de Atividade - Assistir Aula

```mermaid
flowchart TD
    Start([Início]) --> A[Acessar página do curso]

    A --> B{Usuário autenticado?}
    B -->|Não| C[Redirecionar para login]
    C --> End1([Fim - Não autenticado])

    B -->|Sim| D[Verificar matrícula]
    D --> E{Matriculado no curso?}
    E -->|Não| F[Exibir opção de compra]
    F --> End2([Fim - Sem matrícula])

    E -->|Sim| G[Carregar módulos e aulas]
    G --> H[Exibir lista de conteúdo]
    H --> I[Selecionar aula]

    I --> J{Aula publicada?}
    J -->|Não| K[Exibir: Em breve]
    K --> H

    J -->|Sim| L[Buscar dados do vídeo]
    L --> M[Carregar player Bunny Stream]
    M --> N[Iniciar reprodução]

    N --> O[Usuário assiste vídeo]
    O --> P{Aula concluída?}
    P -->|Não| O

    P -->|Sim| Q[Clicar em Marcar como concluída]
    Q --> R[POST /api/progress]
    R --> S[Atualizar LessonProgress]
    S --> T[Recalcular % do curso]

    T --> U{Progresso = 100%?}
    U -->|Sim| V[Liberar certificado]
    U -->|Não| W[Exibir próxima aula]

    V --> End3([Fim - Curso completo])
    W --> I
```

## 4.4 Diagrama de Atividade - Recuperação de Senha

```mermaid
flowchart TD
    Start([Início]) --> A[Acessar recuperar senha]
    A --> B[Informar email]
    B --> C[Submeter formulário]

    C --> D[Buscar usuário por email]
    D --> E{Usuário existe?}
    E -->|Não| F[Exibir mensagem genérica]
    F --> End1([Fim - Email não encontrado])

    E -->|Sim| G[Gerar token único]
    G --> H[Calcular hash do token]
    H --> I[Salvar PasswordResetToken]
    I --> J[Definir expiração: 24h]
    J --> K[Enviar email com link]
    K --> L[Exibir: verifique seu email]

    L --> M[Usuário clica no link]
    M --> N[Acessar página de redefinição]
    N --> O[Validar token]

    O --> P{Token válido?}
    P -->|Não| Q[Exibir: link expirado]
    Q --> End2([Fim - Token inválido])

    P -->|Sim| R{Token já usado?}
    R -->|Sim| Q

    R -->|Não| S[Exibir formulário nova senha]
    S --> T[Preencher nova senha]
    T --> U[Validar força da senha]

    U --> V{Senha forte?}
    V -->|Não| W[Exibir requisitos]
    W --> T

    V -->|Sim| X[Hash da nova senha]
    X --> Y[Atualizar senha do usuário]
    Y --> Z[Marcar token como usado]
    Z --> AA[Exibir: senha alterada]
    AA --> End3([Fim - Sucesso])
```

## 4.5 Diagrama de Atividade - Upload de Vídeo (Admin)

```mermaid
flowchart TD
    Start([Início]) --> A[Admin acessa gestão de aulas]
    A --> B[Selecionar aula para editar]
    B --> C[Clicar em Upload de Vídeo]

    C --> D[Selecionar arquivo de vídeo]
    D --> E{Formato válido?}
    E -->|Não| F[Exibir erro: formato inválido]
    F --> D

    E -->|Sim| G[Criar vídeo no Bunny Stream]
    G --> H[Obter URL de upload]
    H --> I[Atualizar status: UPLOADING]

    I --> J[Iniciar upload do arquivo]
    J --> K[Exibir barra de progresso]
    K --> L{Upload completo?}
    L -->|Não| K

    L -->|Sim| M[Notificar Bunny: upload concluído]
    M --> N[Atualizar status: PROCESSING]
    N --> O[Bunny processa/codifica vídeo]

    O --> P{Processamento ok?}
    P -->|Não| Q[Atualizar status: FAILED]
    Q --> R[Exibir erro]
    R --> End1([Fim - Erro])

    P -->|Sim| S[Obter ID do vídeo Bunny]
    S --> T[Salvar bunnyVideoId na aula]
    T --> U[Atualizar status: COMPLETED]
    U --> V[Exibir: vídeo pronto]
    V --> End2([Fim - Sucesso])
```

---

# 5. DIAGRAMAS DE ESTADOS

## 5.1 Diagrama de Estados - Pagamento

```mermaid
stateDiagram-v2
    [*] --> PENDING: Checkout iniciado

    PENDING --> REQUIRES_ACTION: Ação adicional necessária
    REQUIRES_ACTION --> PENDING: Ação completada
    REQUIRES_ACTION --> CANCELED: Timeout/Cancelamento

    PENDING --> SUCCEEDED: Pagamento confirmado
    PENDING --> CANCELED: Sessão expirada

    SUCCEEDED --> REFUNDED: Reembolso processado

    CANCELED --> [*]
    REFUNDED --> [*]
    SUCCEEDED --> [*]

    note right of PENDING
        Status inicial quando
        sessão Stripe é criada
    end note

    note right of SUCCEEDED
        Gatilho para criar
        matrícula e enviar email
    end note
```

## 5.2 Diagrama de Estados - Pedido (Order Status)

```mermaid
stateDiagram-v2
    [*] --> PENDING_PAYMENT: Pedido criado

    PENDING_PAYMENT --> PAYMENT_CONFIRMED: Pagamento aprovado
    PENDING_PAYMENT --> CANCELED: Pagamento falhou/expirou

    PAYMENT_CONFIRMED --> PROCESSING: Admin revisa pedido

    PROCESSING --> COMPLETED: Curso liberado
    PROCESSING --> CANCELED: Admin cancela

    COMPLETED --> [*]
    CANCELED --> [*]

    note right of PAYMENT_CONFIRMED
        Para cursos digitais,
        pode ir direto para COMPLETED
    end note

    note right of PROCESSING
        Admin revisa e
        confirma a entrega do acesso
    end note
```

## 5.3 Diagrama de Estados - Envio de Produto Físico (Shipping)

```mermaid
stateDiagram-v2
    [*] --> PENDING: Pedido pago

    PENDING --> PREPARING: Admin inicia preparação

    PREPARING --> READY_TO_SHIP: Embalado

    READY_TO_SHIP --> SHIPPED: Coletado pela transportadora

    SHIPPED --> IN_TRANSIT: Em transporte

    IN_TRANSIT --> OUT_FOR_DELIVERY: Saiu para entrega

    OUT_FOR_DELIVERY --> DELIVERED: Entregue com sucesso
    OUT_FOR_DELIVERY --> DELIVERY_FAILED: Entrega falhou

    DELIVERY_FAILED --> RETURNED: Devolvido ao remetente
    DELIVERY_FAILED --> OUT_FOR_DELIVERY: Nova tentativa

    RETURNED --> [*]
    DELIVERED --> [*]

    note right of SHIPPED
        Código de rastreamento
        é adicionado neste estado
    end note

    note right of IN_TRANSIT
        Status sincronizado com
        Correios/Jadlog API
    end note
```

## 5.4 Diagrama de Estados - Conta de Usuário

```mermaid
stateDiagram-v2
    [*] --> REGISTRADO: Cadastro realizado

    REGISTRADO --> ATIVO: Primeiro login

    ATIVO --> ATIVO: Acesso normal
    ATIVO --> EXPIRADO: Data de expiração atingida
    ATIVO --> INATIVO: Admin desativa conta

    EXPIRADO --> ATIVO: Renovação/Compra
    EXPIRADO --> INATIVO: Admin desativa

    INATIVO --> ATIVO: Admin reativa conta

    INATIVO --> [*]

    note right of ATIVO
        Pode acessar cursos
        matriculados
    end note

    note right of EXPIRADO
        Login bloqueado
        Precisa renovar
    end note

    note right of INATIVO
        Conta desativada
        pelo administrador
    end note
```

## 5.5 Diagrama de Estados - Aula (Lesson)

```mermaid
stateDiagram-v2
    [*] --> DRAFT: Aula criada

    DRAFT --> SCHEDULED: Admin agenda publicação
    DRAFT --> PUBLISHED: Admin publica imediatamente

    SCHEDULED --> PUBLISHED: Data agendada atingida
    SCHEDULED --> DRAFT: Admin cancela agendamento

    PUBLISHED --> DRAFT: Admin despublica

    PUBLISHED --> [*]

    note right of DRAFT
        Visível apenas para admin
        Alunos não veem
    end note

    note right of SCHEDULED
        scheduledAt define
        quando será publicada
    end note

    note right of PUBLISHED
        Visível para alunos
        matriculados
    end note
```

## 5.6 Diagrama de Estados - Upload de Vídeo

```mermaid
stateDiagram-v2
    [*] --> PENDING: Admin seleciona vídeo

    PENDING --> UPLOADING: Upload iniciado

    UPLOADING --> PROCESSING: Upload concluído
    UPLOADING --> FAILED: Erro no upload

    PROCESSING --> COMPLETED: Bunny termina codificação
    PROCESSING --> FAILED: Erro no processamento

    FAILED --> PENDING: Tentar novamente

    COMPLETED --> [*]
    FAILED --> [*]

    note right of UPLOADING
        Arquivo sendo enviado
        para Bunny Stream
    end note

    note right of PROCESSING
        Bunny converte para
        múltiplas resoluções (HLS)
    end note
```

## 5.7 Diagrama de Estados - Matrícula (Enrollment)

```mermaid
stateDiagram-v2
    [*] --> ACTIVE: Pagamento confirmado

    ACTIVE --> CANCELLED: Reembolso ou admin cancela

    CANCELLED --> ACTIVE: Admin reativa manualmente

    ACTIVE --> [*]
    CANCELLED --> [*]

    note right of ACTIVE
        Aluno pode acessar
        todas as aulas do curso
    end note

    note right of CANCELLED
        Acesso ao curso
        removido
    end note
```

---

# 6. MODELO DE DADOS SIMPLIFICADO

## 6.1 Entidades Principais e Relacionamentos

```mermaid
erDiagram
    USER ||--o{ ENROLLMENT : "tem"
    USER ||--o{ PAYMENT : "realiza"
    USER ||--o{ ADDRESS : "possui"
    USER ||--o{ LESSON_PROGRESS : "registra"

    COURSE ||--o{ MODULE : "contém"
    COURSE ||--o{ ENROLLMENT : "tem"
    COURSE ||--o{ PAYMENT : "recebe"

    MODULE ||--o{ LESSON : "contém"

    LESSON ||--o{ LESSON_PROGRESS : "tem"

    PAYMENT ||--o{ SHIPPING_HISTORY : "tem"

    USER {
        uuid id PK
        string name
        string email UK
        string passwordHash
        string cpf
        enum role
        boolean isActive
        datetime expiresAt
    }

    COURSE {
        cuid id PK
        string slug UK
        string title
        decimal price
        string trailerVideoId
        boolean isFeatured
    }

    MODULE {
        cuid id PK
        string title
        int order
    }

    LESSON {
        cuid id PK
        string title
        string bunnyVideoId
        int duration
        enum publishStatus
    }

    ENROLLMENT {
        cuid id PK
        enum status
    }

    PAYMENT {
        cuid id PK
        decimal amount
        enum status
        enum orderStatus
        enum productType
        string trackingCode
        enum shippingStatus
    }

    ADDRESS {
        cuid id PK
        string postalCode
        string city
        string state
        boolean isDefault
    }

    LESSON_PROGRESS {
        cuid id PK
        boolean completed
    }

    SHIPPING_HISTORY {
        cuid id PK
        enum shippingStatus
        string location
        string description
    }
```

---

# 7. RESUMO PARA APRESENTAÇÃO

## 7.1 Pontos-Chave do Sistema

1. **Plataforma EAD** especializada em cursos de harmonização facial
2. **Arquitetura moderna** com Next.js 15, React 19 e TypeScript
3. **Pagamentos seguros** via Stripe com webhooks
4. **Streaming de vídeo** via Bunny Stream CDN
5. **Controle de acesso** baseado em roles (Aluno/Admin)
6. **Rastreamento de progresso** por aula e certificado automático
7. **Integração logística** com Correios e Jadlog para produtos físicos

## 7.2 Atores do Sistema

| Ator | Descrição |
|------|-----------|
| **Aluno** | Usuário que se cadastra, compra e acessa cursos |
| **Administrador** | Gerencia cursos, aulas, alunos e pedidos |
| **Stripe** | Sistema externo de processamento de pagamentos |
| **Bunny Stream** | Sistema externo de hospedagem de vídeos |
| **Correios/Jadlog** | Sistemas externos de rastreamento de entregas |
| **Resend** | Sistema externo de envio de emails |

## 7.3 Principais Fluxos

1. **Cadastro → Compra → Acesso** - Jornada do aluno
2. **Upload → Publicação → Consumo** - Ciclo de vida do conteúdo
3. **Pedido → Pagamento → Entrega** - Processo de vendas
4. **Progresso → Conclusão → Certificado** - Gamificação educacional

---

*Documentação gerada para apresentação acadêmica/profissional da Plataforma Taty*
