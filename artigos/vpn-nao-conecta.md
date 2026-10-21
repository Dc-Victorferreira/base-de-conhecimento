# VPN não conecta: checklist de 8 verificações

## Quando usar

- Cliente VPN recusa autenticação.
- Conecta e cai em segundos.
- Conecta, mas o usuário não acessa os sistemas internos.

## Pré-requisitos

- Saber qual cliente é usado (Windows nativo, FortiClient, GlobalProtect, Cisco AnyConnect...).
- Ter o usuário disponível: a maioria dos testes exige a senha dele, e você não deve pedir a senha.

## Ordem de verificação (pare no primeiro que falhar)

1. **Internet funciona?** Abra um site público. Sem internet, não há VPN.
2. **Endereço do servidor correto?** Confira o host no cliente (ex.: `vpn.empresa.com.br`). Um caractere errado derruba tudo.
3. **Credenciais e MFA.** Senha expirada, conta bloqueada ou token expirado aparecem como "falha de autenticação". Verifique a conta no AD antes de reinstalar qualquer coisa.
4. **Relógio do computador.** Diferença acima de 5 minutos quebra autenticação por certificado. `w32tm /resync` resolve.
5. **Certificado.** Data de validade vencida ou certificado não confiável → o cliente recusa antes de autenticar.
6. **Firewall/antivírus local.** Teste com o usuário em outra rede (4G do celular). Se funciona fora da rede da empresa, o bloqueio é de rede, não da máquina.
7. **Cliente corrompido.** Desinstale, reinicie e reinstale a versão indicada pela TI. Não instale versão mais nova que a homologada.
8. **Perfil do usuário no cliente.** Perfis antigos guardam configuração e certificado velhos; recriar o perfil resolve boa parte dos "conecta e cai".

## Como confirmar que resolveu

- Cliente mostra **Conectado** por mais de 5 minutos.
- `ping` no servidor interno responde.
- Usuário abre o sistema que precisava (e-mail interno, ERP, pasta de rede).

Conectar não é resolver. A confirmação é o acesso ao recurso.

## Quando escalar

- Vários usuários na mesma unidade → servidor, link ou firewall. Não é atendimento individual.
- Falha só com um usuário, em qualquer rede e qualquer máquina → conta/perfil no servidor de VPN.
- Suspeita de certificado comprometido ou tentativa de acesso estranha → segurança da informação, imediatamente.

## O que nunca fazer

- Pedir a senha do usuário para "testar".
- Instalar cliente de origem desconhecida para "ver se resolve".
- Desativar antivírus para testar conexão.

## Testado em

Cliente VPN corporativo em Windows 11, rede doméstica e rede corporativa.

**Última atualização:** 21/10/2026
