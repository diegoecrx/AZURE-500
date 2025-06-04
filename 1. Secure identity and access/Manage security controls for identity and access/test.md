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

Este resumo serve como guia rápido e estruturado para preparação do exame de certificação AZ-500, abrangendo práticas recomendadas e ferramentas específicas do ambiente Microsoft Azure.
