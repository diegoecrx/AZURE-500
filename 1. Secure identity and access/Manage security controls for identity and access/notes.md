# Microsoft Cloud Security Benchmark: Identity Management and Privileged Access

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




