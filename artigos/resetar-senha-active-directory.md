# Resetar senha de usuário no Active Directory

## Quando usar

- Usuário esqueceu a senha.
- A senha expirou e ele não consegue trocar sozinho.
- A senha atual não atende à política (tamanho ou complexidade).

**Não use** quando a conta estiver apenas bloqueada (veja o artigo de desbloqueio) nem quando o problema for "não consigo logar" sem confirmação de que a senha é a causa.

## Pré-requisitos

- Acesso ao Active Directory com permissão de reset no OU do usuário.
- Identidade confirmada por um segundo canal (ramal, gestor ou presencial). **Nunca** resetar senha a pedido de quem ligou sem verificação.
- Usuário disponível para testar o login em seguida.

## Passo a passo

### Pela interface (ADUC)

1. Abra `dsa.msc` (Usuários e Computadores do Active Directory).
2. Localize o usuário na árvore do domínio.
3. Clique com o botão direito → **Redefinir Senha**.
4. Digite a senha temporária e confirme.
5. Marque **O usuário deve alterar a senha no próximo logon**.
6. Desmarque **Desbloquear a conta do usuário** apenas se ela estiver bloqueada e você não quiser liberar ainda.
7. **OK** → informe a senha temporária ao usuário por canal acordado (nunca por e-mail em texto aberto).

### Pelo PowerShell

```powershell
Set-ADAccountPassword -Identity "joao.silva" -Reset `
  -NewPassword (Read-Host -AsSecureString "Senha temporaria")

Set-ADUser -Identity "joao.silva" -ChangePasswordAtLogon $true
```

## Como confirmar que resolveu

```powershell
Get-ADUser "joao.silva" -Properties PasswordLastSet, PasswordExpired, LockedOut |
  Select-Object Name, PasswordLastSet, PasswordExpired, LockedOut
```

- `PasswordLastSet` deve mostrar a hora atual.
- `PasswordExpired` deve estar `True` (o usuário troca no próximo logon).
- Peça ao usuário que faça login com a senha temporária e crie a nova. Confirmação verbal ou por chamado, com registro.

## Quando escalar

- O usuário não recebe a senha temporária (problema de comunicação, não de AD).
- O reset não persiste: a conta volta a expirar ou bloquear em minutos → investigar sincronização, conta de serviço ou credencial antiga em celular.
- A conta é de serviço ou de aplicação: não resetar sem o dono do sistema; o reset derruba integração.

## Erros comuns

- Resetar sem confirmar identidade — é falha de segurança, não de suporte.
- Esquecer de marcar "alterar no próximo logon" e deixar senha conhecida circulando.
- Resetar e não avisar o usuário: ele continua tentando a senha antiga e bloqueia a conta de novo.

## Testado em

Domínio de laboratório `lab.local` — Windows Server 2022 + cliente Windows 11.

**Última atualização:** 21/10/2026
