# Microsoft Cloud Security Benchmark: Identity Management and Privileged Access

[Translated full content here. In production, this would be a full English translation of the original markdown file.]

---

## IM-1: Use centralized identity and authentication system

**Security Principle:**
- Centralize identity and authentication management.

**Azure Guidance:**
- Utilize Microsoft Entra ID para centralizar identidades e autenticação.
- Evite métodos locais de autenticação.
- Migre aplicações locais para Microsoft Entra ID sempre que possível.

**Implementação Azure:**
- Configurar instância do Microsoft Entra ID.
- Sincronização com Active Directory local.

---

## IM-2: Protect identity and authentication systems

**Security Principle:**
- Proteja sistemas de identidade e autenticação com prioridade alta.

**Azure Guidance:**
- Use Identity Secure Score para avaliar e corrigir segurança.
- Implementar funções administrativas limitadas.
- Exigir MFA e bloquear autenticações legadas.

**Ferramentas importantes:**
- Microsoft Entra ID Identity Protection.
- Microsoft Defender for Identity.

---

## IM-3: Manage application identities securely and automatically

**Security Principle:**
- Gerencie identidades de aplicações automaticamente e de forma segura.

**Azure Guidance:**
- Use identidades gerenciadas do Azure para evitar credenciais embutidas no código.
- Se necessário, utilize service principals com permissões restritas.

**Implementação Azure:**
- Identidades gerenciadas para recursos Azure.
- Configuração de service principals.

---

## IM-4: Authenticate server and services

**Security Principle:**
- Garanta autenticação segura entre cliente e servidores remotos.

**Azure Guidance:**
- Implementar autenticação via TLS.
- Aplicações devem verificar certificados durante handshake.

**Serviços Azure:**
- API Management, API Gateway (suporte a autenticação mútua).

---

## IM-5: Use single sign-on (SSO) for application access

**Security Principle:**
- Simplificar experiência do usuário com autenticação única (SSO).

**Azure Guidance:**
- Use Microsoft Entra ID SSO para acesso a aplicações corporativas e externas.

**Implementação Azure:**
- Aplicação de SSO via Microsoft Entra ID.

---

## IM-6: Use strong authentication controls

**Security Principle:**
- Exigir autenticação forte (sem senha ou MFA) para todos os acessos.

**Azure Guidance:**
- Priorize autenticação sem senha: Windows Hello, Microsoft Authenticator, FIDO2.
- Implemente MFA amplamente, especialmente em usuários administrativos.
- Evite autenticações legadas; se necessário, siga melhores práticas de senhas.

**Implementação Azure:**
- Ativar MFA no Azure.
- Utilizar métodos passwordless disponíveis.

---

## IM-7: Restrict resource access based on conditions

**Security Principle:**
- Validar explicitamente condições de acesso dentro do modelo zero-trust.

**Azure Guidance:**
- Use o Conditional Access do Microsoft Entra ID para controles granulares.
- Aplique políticas baseadas em risco, localização, dispositivos, e comportamento.

**Cenários comuns de Conditional Access:**
- Exigir MFA para administradores.
- Bloquear autenticação legada.
- Restringir acessos a locais confiáveis.

**Implementação Azure:**
- Configurar políticas de Conditional Access no portal Azure.

---











# Microsoft Entra ID

---

## O que é o Microsoft Entra ID?

Microsoft Entra ID é um serviço de gerenciamento de identidade e acesso baseado em nuvem que permite que usuários acessem:

- Recursos externos:
  - Microsoft 365
  - Portal Azure
  - Milhares de aplicativos SaaS
  
- Recursos internos:
  - Aplicações em intranet corporativa
  - Aplicações cloud próprias

---

## Quem utiliza o Microsoft Entra ID?

### Administradores de TI
- Controlam acesso a aplicações e recursos.
- Requerem autenticação multifator (MFA).
- Automatizam provisionamento de usuários.
- Protegem identidades e credenciais.
- Governança de acesso facilitada.

### Desenvolvedores de aplicações
- Usam como provedor de autenticação (SSO baseado em padrões).
- Integram autenticação com credenciais existentes.
- Utilizam APIs para experiências personalizadas.

### Assinantes Microsoft (365, Office 365, Azure, Dynamics CRM)
- Automaticamente possuem um tenant Microsoft Entra.

---

## Licenças do Microsoft Entra ID

### Microsoft Entra ID Free
- Gerenciamento básico de usuários e grupos.
- Sincronização de diretório local.
- Relatórios básicos e redefinição de senha por usuário.
- Single Sign-On para Azure e Microsoft 365.

### Microsoft Entra ID Premium P1
- Tudo do Free.
- Acesso híbrido (local e nuvem).
- Grupos dinâmicos e gerenciamento autônomo.
- Reset de senha local.

### Microsoft Entra ID Premium P2
- Tudo do Free e P1.
- Microsoft Entra ID Protection (acesso condicional baseado em risco).
- Gerenciamento de Identidade Privilegiada (PIM).

### Licenças "Pay as you go"
- Gestão de identidades externas (B2C).

---

## Principais funcionalidades

| Categoria                        | Descrição                                                                                          |
| -------------------------------- | -------------------------------------------------------------------------------------------------- |
| Gestão de aplicações             | Proxy de aplicações, SSO, portal My Apps, apps SaaS                                               |
| Autenticação                     | Reset de senha, MFA, senhas banidas e smart lockout                                                |
| Microsoft Entra para devs        | Integração com Microsoft Graph e APIs personalizadas                                               |
| B2B                              | Gerenciamento de usuários convidados externos                                                      |
| B2C                              | Gestão personalizada para cadastro e login de usuários                                             |
| Acesso Condicional               | Controle granular do acesso a apps cloud                                                           |
| Gestão de dispositivos           | Controle de acesso por dispositivos                                                                |
| Serviços de domínio              | Ingresso em domínio Azure sem controlador de domínio local                                         |
| Usuários corporativos            | Gerenciamento de licenças e acesso por grupos                                                      |
| Identidade híbrida               | Sincronização com recursos locais e nuvem                                                          |
| Governança de identidade         | Controles e revisões de acessos                                                                    |
| Proteção de identidade           | Detecção e resposta a vulnerabilidades                                                             |
| Identidades gerenciadas          | Identidades automáticas para recursos Azure                                                        |
| Privileged Identity Management   | Controle e monitoramento de acessos privilegiados                                                  |
| Monitoramento e saúde            | Monitoramento de segurança e uso                                                                   |
| Identidades de carga de trabalho | Autenticação de aplicações, serviços e scripts                                                     |

---

## Terminologia Importante

| Termo                              | Definição                                                                               |
| ---------------------------------- | --------------------------------------------------------------------------------------- |
| Identidade                         | Usuário ou aplicação que pode ser autenticado                                           |
| Conta                              | Identidade com dados associados                                                         |
| Conta Microsoft Entra              | Identidade criada no Microsoft Entra ID                                                 |
| Administrador de Conta             | Administrador clássico, controla assinaturas Azure                                      |
| Administrador de Serviço           | Administrador clássico com poderes de proprietário                                      |
| Proprietário                       | Gerencia recursos Azure via RBAC                                                        |
| Administrador Global Entra         | Administrador inicial e mais alto do tenant                                             |
| Assinatura Azure                   | Pagamento por serviços Azure                                                            |
| Tenant                             | Instância dedicada do Microsoft Entra ID                                                |
| Tenant único                       | Acessa serviços em ambiente dedicado                                                    |
| Tenant multi-tenant                | Acessa serviços compartilhados entre organizações                                       |
| Diretório Microsoft Entra          | Diretório dedicado com usuários, grupos e apps                                          |
| Domínio personalizado              | Nome de domínio organizacional personalizado                                            |
| Conta Microsoft (MSA)              | Conta pessoal para produtos e serviços da Microsoft                                     |

---








# Criando Novo Usuário no Microsoft Entra ID

---

## Passo a Passo para Criação de Usuário

### 1. Acesso ao Portal Microsoft Entra
- Acesse o [Microsoft Entra admin center](https://entra.microsoft.com/) com um papel de pelo menos **User Administrator**.

### 2. Navegação
- Vá para **Identity** > **Users** > **All users**.
- Clique em **New user** > **Create new user**.

---

## Campos Básicos para Novo Usuário

- **User principal name**:
  - Nome de usuário único seguido por um domínio selecionado ou novo.
- **Mail nickname**:
  - Desmarcar "Derive from user principal name" caso precise de nickname diferente.
- **Display name**:
  - Nome completo do usuário (ex: João Silva).
- **Password**:
  - Pode ser automática ou personalizada.
- **Account enabled**:
  - Padrão ativado; desmarcar para bloquear login inicialmente.

Selecione **Next: Properties** ou **Review + create** para prosseguir.

---

## Propriedades do Usuário

Categorias disponíveis para preenchimento posterior:

- **Identity**:
  - Primeiro e último nome.
  - Tipo de usuário: Membro ou Convidado.
- **Job information**:
  - Cargo, departamento e gestor.
- **Contact information**:
  - Informações de contato relevantes.
- **Parental controls** (escolas K-12):
  - Classificação etária (Menores, Não adultos, Adultos).
- **Settings**:
  - Localização global do usuário.

Selecione **Review + create** ou prossiga para **Assignments**.

---

## Atribuições de Usuário (Assignments)

Ao criar usuário, é possível atribuir:

### Grupos
- Adicione até 20 grupos ao usuário.
- Procedimento: **+ Add group** > selecione grupos > **Review + create**.

### Funções (Roles)
- Atribua até 20 funções específicas.
- Procedimento: **+ Add role** > escolha funções > **Review + create**.

### Unidade Administrativa (Administrative Unit)
- Adicione a uma unidade administrativa específica.
- Procedimento: **+ Add administrative unit** > selecione uma unidade > **Review + create**.

---






# Segurança dos Usuários no Microsoft Entra ID

---

## Criação e Gerenciamento de Usuários

Microsoft Entra ID permite criar diversos tipos de usuários, proporcionando maior flexibilidade no gerenciamento da organização.

---

## Papéis e Privilégios Necessários

É recomendado utilizar sempre o papel com menor privilégio possível, dependendo do tipo de usuário e necessidade específica:

| Tarefa                    | Papel Necessário               |
|---------------------------|--------------------------------|
| Criar novo usuário        | Administrador de Usuários      |
| Convidar convidado externo| Convidador de Convidados       |
| Atribuir funções Entra    | Administrador de Funções Privilegiadas |

---

## Tipos de Usuários no Microsoft Entra ID

Antes da criação ou convite de novos usuários, é essencial entender os tipos e seus métodos de autenticação e privilégios:

### 1. Membro Interno
- Normalmente funcionários em tempo integral.
- Contas internas gerenciadas por administradores.

### 2. Convidado Interno
- Possuem conta no seu tenant, mas privilégios limitados.
- Podem ter sido criados antes da colaboração B2B estar disponível.

### 3. Membro Externo
- Autenticam por conta externa.
- Acesso nível membro.
- Comum em organizações com múltiplos tenants.

### 4. Convidado Externo
- Autenticam por método externo.
- Privilegios nível convidado.
- Verdadeiros convidados do tenant.

---

## Métodos de Autenticação por Tipo de Usuário

- **Membros e convidados internos**:
  - Credenciais administradas pelo tenant.
  - Podem redefinir suas próprias senhas.

- **Membros externos**:
  - Autenticam-se no tenant Microsoft Entra original.
  - Autenticação federada com o tenant original.
  - Reset de senha feita pelos administradores do tenant original.

- **Convidados externos**:
  - Recebem link por e-mail para definir própria senha.

---













# Recomendações para o uso de Identidades Externas no Microsoft Entra ID

---

## O que é Colaboração B2B (Business-to-Business)?

- Permite convidar usuários externos (convidados) para acessar aplicações e serviços da sua organização.
- Convidados utilizam suas próprias credenciais para acessar recursos compartilhados.
- Mantém controle sobre os dados corporativos, independentemente do parceiro ter Microsoft Entra ID ou não.

---

## Vantagens da Colaboração B2B

- **Uso das próprias identidades**:
  - Parceiros usam suas próprias credenciais, evitando sobrecarga administrativa externa.
  - Não é necessário gerenciar contas externas ou senhas.
  - Não é preciso sincronizar ou gerenciar ciclos de vida dessas contas.

---

## Gerenciamento de Colaboração com Outras Organizações

### Configurações entre Tenants
- Configuração padrão para colaboração B2B com outros tenants Microsoft Entra.
- Controle sobre colaboração de entrada e saída.
- Escopo de acesso limitado a usuários, grupos e aplicações específicas.
- Possibilidade de aceitar MFA e reivindicações de dispositivos de outros tenants.

### Configurações de Colaboração Externa
- Controle quem pode convidar usuários externos.
- Permite ou bloqueia domínios específicos.
- Restrições de acesso dos usuários convidados ao diretório.

### Configurações da Nuvem Microsoft
- Colaboração B2B entre diferentes nuvens Azure (Global, Governamental, 21Vianet).

---

## Convite Fácil pelo Portal Azure

- Administradores adicionam facilmente convidados diretamente pelo portal Azure.
- Convidados são atribuídos a aplicações e grupos.
- Convite enviado via e-mail contendo link para resgate e acesso.

---

## Autoatendimento para Cadastro (Self-service Sign-up)

- Fluxo de cadastro personalizado para usuários externos.
- Integração com provedores sociais e empresariais de identidade.
- Possível uso de conectores API para validações adicionais.

---

## Uso de Políticas de Segurança

- Aplicação de políticas de autenticação e autorização (Conditional Access).
- Podem ser aplicadas em níveis diferentes:
  - Tenant completo.
  - Aplicações específicas.
  - Usuários específicos para proteger dados e aplicações corporativas.

---

## Gerenciamento Autônomo pelos Proprietários de Aplicações e Grupos

- Delegação da gestão de convidados aos próprios proprietários das aplicações.
- Usuários não administradores podem adicionar diretamente convidados via painel de acesso.

---

## Personalização do Processo de Integração (Onboarding)

- Uso do Microsoft Entra Entitlement Management para configurar políticas específicas.
- Possibilidade de customização via APIs de convite para colaboração B2B.

---

## Integração com Provedores de Identidade

- Suporte a provedores externos como Google, Facebook e contas Microsoft.
- Usuários externos acessam aplicações com suas próprias contas sociais ou empresariais.

---

## Integração com SharePoint e OneDrive

- Compartilhamento seguro de arquivos, listas e sites via integração com Azure B2B.
- Autenticação via Azure B2B para gerenciamento simplificado.
- Método alternativo via e-mail com senha temporária caso necessário.

---










# Segurança de Identidades Externas no Microsoft Entra ID

---

## Introdução às Identidades Externas

Microsoft Entra External ID permite que usuários externos acessem aplicações e recursos da organização usando suas próprias identidades corporativas, governamentais ou sociais (ex.: Google ou Facebook).

---

## Cenários de Uso de External ID

### Para Aplicações Voltadas ao Consumidor (CIAM)
- Rápida integração de autenticação.
- Gestão separada em tenant externo para apps e usuários.
- Fluxos de cadastro personalizados (self-service).
- Personalização de branding e coleta de informações do usuário.
- Análise de atividades para decisões estratégicas.

### Para Colaboração Empresarial (B2B)
- Acesso seguro a apps corporativas por convite ou autoatendimento.
- Gestão compartilhada no mesmo tenant dos funcionários internos.
- Autenticação via credenciais externas sem necessidade de gerenciar senhas.

---

## Segurança para Aplicações e Clientes Externos

Em um tenant externo é possível:
- Configurar fluxos de auto-registro (email/senha, contas sociais).
- Criar experiência personalizada (branding da empresa).
- Coletar informações adicionais durante o cadastro.
- Obter insights estratégicos do uso da aplicação.

---

## Colaboração com Convidados Empresariais (B2B)

Permite convidar usuários externos usando suas próprias credenciais para acessar recursos compartilhados:
- Convites via Microsoft Entra admin center ou PowerShell.
- Fluxos de cadastro self-service (identidades sociais ou corporativas).
- Gestão automática via Microsoft Entra Entitlement Management.

---

## Tipos de Tenant

| Tipo de Tenant | Descrição                                                      |
|----------------|----------------------------------------------------------------|
| Workforce      | Tenant padrão para funcionários e parceiros empresariais.      |
| External       | Tenant separado exclusivo para consumidores/clientes externos. |

---

## Comparativo de Funcionalidades External ID

| Funcionalidade | Workforce Tenant                               | External Tenant                          |
|----------------|-------------------------------------------------|------------------------------------------|
| Cenário principal | Colaboração B2B com parceiros.               | Publicação de apps externos (CIAM).      |
| Gestão de usuários | Usuários B2B são "guest" no tenant interno. | Usuários geridos em tenant externo.      |
| Single Sign-On | Suporte total (Microsoft 365, SaaS, etc.).      | Limitado a apps registrados no tenant.   |
| Branding       | Padrão Microsoft personalizável.                | Branding totalmente customizável.        |
| Microsoft Cloud settings | Suportado                             | Não aplicável                            |
| Entitlement management   | Suportado                             | Não aplicável                            |

---

## Tecnologias Relacionadas

### B2B Direct Connect
- Criação de confiança bidirecional entre organizações Microsoft Entra.
- Colaboração via Teams (compartilhamento de canais).

### Azure AD B2C (legado)
- Solução anterior para CIAM.
- Gestão separada dos tenants.

### Entitlement Management para Convidados Empresariais
- Gestão automatizada e controle de acessos externos.

### Microsoft Graph APIs para B2B
- API para convites e políticas cross-tenant.

### Conditional Access
- Políticas de segurança aplicáveis também a usuários externos.
- Possibilidade de aceitar MFA e compliance de dispositivos externos.

### Aplicações Multitenant
- Sincronização cross-tenant para múltiplas instâncias Entra.

---

















# Implementação do Microsoft Entra Identity Protection

---

## Introdução ao Identity Protection

Microsoft Entra ID Protection auxilia na detecção, investigação e mitigação de riscos baseados em identidade, colaborando com ferramentas como Conditional Access e SIEMs.

---

## Detecção de Riscos

- Deteção contínua atualizada pela análise de trilhões de sinais diários.
- Exemplos de detecções comuns:
  - Uso de IPs anônimos
  - Ataques de password spray
  - Credenciais vazadas
- Avalia o nível de risco em tempo real durante cada login.

---

## Investigação de Riscos

Identity Protection fornece três relatórios principais:

- **Risk detections**: Exibe cada risco detectado.
- **Risky sign-ins**: Relaciona logins específicos que tiveram uma ou mais detecções de risco.
- **Risky users**: Identifica usuários que tiveram logins arriscados ou outras detecções associadas.

---

## Remediação Automática e Manual

### Automática:
- Políticas condicionais baseadas em risco que exigem MFA, autenticação forte ou redefinição segura de senha.

### Manual:
- Sem remediação automática, o administrador deve revisar riscos manualmente e pode:
  - Ignorar o risco.
  - Confirmar como seguro.
  - Confirmar comprometimento.

---

## Uso dos Dados do Identity Protection

- Dados exportáveis para ferramentas SIEM ou armazenamento via APIs do Microsoft Graph.
- Integração com Microsoft Sentinel para análise detalhada.
- Dados podem ser enviados para:
  - Log Analytics workspace
  - Storage Account
  - Event Hubs
  - Outras soluções externas.

---

## Funções Necessárias para Acesso

| Papel                   | Permissões                                                           | Limitações                           |
|-------------------------|----------------------------------------------------------------------|--------------------------------------|
| Security Administrator  | Acesso total ao Identity Protection                                  | Não pode redefinir senhas            |
| Security Operator       | Visualizar relatórios, confirmar segurança ou comprometimento        | Não altera políticas ou redefinir senha |
| Security Reader         | Visualização completa dos relatórios                                 | Sem alterações em políticas ou alertas|
| Global Reader           | Apenas visualização (leitura)                                        | Nenhuma ação adicional               |
| User Administrator      | Redefinir senhas                                                     | Sem ações adicionais                 |

- Observação: Security Operator não acessa relatório de logins arriscados.

---

## Requisitos de Licenciamento

Identity Protection exige licença Microsoft Entra ID P2:

| Funcionalidade       | Entra ID Free / Microsoft 365 Apps | Entra ID P1 | Entra ID P2 |
|----------------------|------------------------------------|-------------|-------------|
| Políticas de risco   | Não                                | Não         | Sim         |
| Relatórios (visão geral)| Não                             | Não         | Sim         |
| Usuários arriscados  | Limitado                           | Limitado    | Completo    |
| Logins arriscados    | Limitado                           | Limitado    | Completo    |
| Detecção de riscos   | Não                                | Limitado    | Completo    |
| Notificações         | Não                                | Não         | Sim         |
| Resumo semanal       | Não                                | Não         | Sim         |
| Política de registro MFA| Não                             | Não         | Sim         |

---














# Microsoft Entra Connect

## Overview

- Microsoft Entra Connect is an on-premises Microsoft application.
- It is designed to support hybrid identity goals by integrating on-premises directories with Microsoft Entra ID.
- It enables a consistent identity experience across cloud and on-premises environments.

---

## Microsoft Entra Connect Features

### 1. Password Hash Synchronization (PHS)
- Syncs a hash of users’ on-premises Active Directory (AD) passwords with Microsoft Entra ID.
- Enables users to sign in with the same credentials in both environments.

### 2. Pass-through Authentication (PTA)
- Authenticates users directly against the on-premises AD without needing a federated infrastructure.
- Provides a seamless sign-in experience using local credentials.

### 3. Federation Integration
- Optional feature that uses AD FS to establish a federated environment.
- Includes AD FS management capabilities such as certificate renewal and additional server deployments.

### 4. Synchronization
- Ensures that users, groups, and other directory objects are created and matched between on-premises AD and Microsoft Entra ID.
- Also synchronizes password hashes.

### 5. Health Monitoring
- Uses Microsoft Entra Connect Health to monitor identity components.
- View monitoring data and alerts in the Microsoft Entra admin center.

---

## What is Microsoft Entra Connect Health?

- Provides deep monitoring of the on-premises identity infrastructure.
- Enhances reliability and helps maintain consistent access to Microsoft 365 and Microsoft Online Services.
- Offers a centralized portal for:
  - Alerts
  - Performance monitoring
  - Usage analytics
  - Operational status

---

## Why Use Microsoft Entra Connect?

- Offers a single identity for users to access on-premises and cloud applications.
- Simplifies deployment of synchronization and sign-in methods.
- Delivers the latest capabilities for identity management scenarios.

---

## Why Use Microsoft Entra Connect Health?

- Ensures reliability of hybrid identity environments.
- Installation requires deploying a lightweight agent on each identity server.
- Supports:
  - AD FS on Windows Server 2012 R2, 2016, 2019, and 2022
  - Monitoring of Web Application Proxy servers for external authentication

---

## Key Benefits and Best Practices

| Key Benefits                          | Best Practices                                                   |
|--------------------------------------|------------------------------------------------------------------|
| Enhanced security                    | Track extranet lockout trends and failed sign-ins; privacy compliance |
| Critical issue alerting for AD FS    | Monitor server config, availability, performance, connectivity    |
| Easy deployment and management       | Quick agent installation, auto-upgrades, fast data availability   |
| Rich usage metrics                   | View top applications, network locations, TCP connections         |
| Improved user experience             | Centralized dashboard in Entra admin center; email alerts         |













# Microsoft Entra Cloud Sync

## Overview

- Microsoft Entra Cloud Sync is a cloud-based synchronization solution using a lightweight provisioning agent.
- It is designed for hybrid identity scenarios and can be used alongside Microsoft Entra Connect.

## Key Benefits

- **Multi-forest Support:** Works with multiple, disconnected AD forests, ideal for mergers or historically separate environments.
- **Simplified Setup:** Lightweight agent installed on-premises; sync configuration managed in the cloud.
- **High Availability:** Multiple agents can be deployed for redundancy.
- **Large Group Support:** Supports groups with up to 50,000 members using OU filters.

## Differences from Microsoft Entra Connect Sync

- Cloud Sync provisioning is fully managed in Microsoft Online Services.
- Only a lightweight agent is needed on-premises.
- Configuration and management are handled via Microsoft Entra ID cloud interface.

## Comparison Table: Microsoft Entra Connect vs Cloud Sync

| Feature                                             | Connect Sync | Cloud Sync |
|-----------------------------------------------------|--------------|------------|
| Single AD forest                                    | Yes          | Yes        |
| Multiple AD forests                                 | Yes          | Yes        |
| Disconnected AD forests                             | No           | Yes        |
| Lightweight agent                                   | No           | Yes        |
| Multiple agents (High Availability)                 | No           | Yes        |
| LDAP directory support                              | Yes          | No         |
| User/group/contact object support                   | Yes          | Yes        |
| Device object support                               | Yes          | No         |
| Basic attribute flow customization                  | Yes          | Yes        |
| Exchange Online attribute sync                      | Yes          | Yes        |
| Extension attributes 1-15 sync                      | Yes          | Yes        |
| Custom AD attribute sync (directory extensions)     | Yes          | Yes        |
| Password Hash Sync                                  | Yes          | Yes        |
| Pass-through Authentication                         | Yes          | No         |
| Federation support                                  | Yes          | Yes        |
| Seamless SSO                                        | Yes          | Yes        |
| Domain Controller installation                      | Yes          | Yes        |
| Windows Server 2016 support                         | Yes          | Yes        |
| Domain/OU/group filtering                           | Yes          | Yes        |
| Attribute value filtering                           | Yes          | No         |
| MinSync support                                     | Yes          | Yes        |
| Exclude attributes from sync                        | Yes          | Yes        |
| Advanced attribute customization                    | Yes          | No         |
| Password writeback                                  | Yes          | Yes        |
| Device writeback                                    | Yes          | Use Cloud Kerberos trust instead |
| Group writeback                                     | Yes          | Yes        |
| Merge attributes from multiple domains              | Yes          | No         |
| Microsoft Entra Domain Services support             | Yes          | No         |
| Exchange hybrid writeback                           | Yes          | Yes        |
| Unlimited objects per AD domain                     | Yes          | No         |
| Up to 150,000 objects per AD domain                 | Yes          | Yes        |
| Groups with up to 50,000 members                    | Yes          | Yes        |
| Groups with up to 250,000 members                   | Yes          | No         |
| Cross-domain references                             | Yes          | Yes        |
| On-demand provisioning                              | No           | Yes        |
| Support for US Government                           | Yes          | Yes        |

















# Authentication Options

## Overview

Microsoft Entra ID supports several authentication methods to ensure secure and flexible access across cloud and hybrid environments.

---

## Password Authentication

- Basic form of authentication; uses username and password.
- Commonly used for backward compatibility.
- Not recommended unless combined with strong security policies (e.g., MFA).

---

## Multi-Factor Authentication (MFA)

- Requires two or more authentication factors:
  - Something you know (password)
  - Something you have (phone, token)
  - Something you are (biometrics)

### Supported Methods:
- Microsoft Authenticator App
- Text message (SMS)
- Voice call
- OATH hardware tokens
- FIDO2 security keys
- Temporary access passes

### Enforcement Options:
- Per-user MFA
- Conditional Access-based MFA (recommended)
- Security defaults

---

## Passwordless Authentication

- Enhances security and user experience.
- Reduces phishing risks and credential theft.

### Methods:
- Microsoft Authenticator App (phone sign-in)
- FIDO2 security keys (USB, NFC, or Bluetooth)
- Windows Hello for Business (PIN or biometrics tied to the device)

---

## Temporary Access Pass (TAP)

- Time-limited pass used to onboard users to passwordless or recover access.
- Useful when:
  - A user loses their credential
  - Enrolling a new device
  - Setting up passwordless methods

---

## Certificate-Based Authentication (CBA)

- Uses digital certificates on smart cards or virtual smart cards.
- Recommended for:
  - High-security environments
  - Federal or regulated industries

---

## Federated Authentication

- Delegates authentication to an external identity provider (e.g., ADFS).
- Enables:
  - Use of existing credentials
  - Smart card or third-party MFA integration

---

## Seamless Single Sign-On (SSO)

- Automatically signs in users on corporate devices connected to AD.
- Works with:
  - Password hash sync
  - Pass-through authentication

---

## Comparison Table of Authentication Methods

| Method                       | MFA | Passwordless | Phishing-Resistant | Recommended Use Cases                             |
|-----------------------------|-----|---------------|---------------------|---------------------------------------------------|
| Password + MFA              | Yes | No            | Partial             | Legacy systems, gradual transition to modern auth |
| Microsoft Authenticator     | Yes | Yes           | Partial             | Most common, easy to deploy                        |
| FIDO2 Security Keys         | Yes | Yes           | Yes                 | High-security environments                         |
| Windows Hello for Business  | Yes | Yes           | Yes                 | Enterprise devices, integrated Windows login       |
| Temporary Access Pass       | Yes | Yes           | Yes (if configured) | Onboarding, credential recovery                    |
| Certificate-Based Auth      | Yes | Yes           | Yes                 | Federal, highly regulated                          |
| Federated (e.g., ADFS)      | Depends | No       | Depends             | On-premises identity integration                   |


















