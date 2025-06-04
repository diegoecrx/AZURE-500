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











# Resumo de Estudo: Microsoft Entra ID

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



