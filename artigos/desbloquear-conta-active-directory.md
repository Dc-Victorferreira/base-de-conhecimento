# Desbloquear conta de usuário no Active Directory

## Quando usar

- A mensagem é "sua conta foi bloqueada" após várias tentativas de senha.
- O usuário jura que digitou a senha certa.
- A conta bloqueia repetidamente sem o usuário estar tentando.

Bloqueio não é o mesmo que senha expirada: desbloquear não resolve senha vencida.

## Pré-requisitos

- Permissão de desbloqueio no OU do usuário.
- Saber **desde quando** e **de onde** vêm as tentativas (VPN, celular, mapeamento de rede, outro computador).

## Passo a passo

### Pela interface

1. Abra `dsa.msc`.
2. Localize o usuário → botão direito → **Propriedades** → aba **Conta**.
3. Marque **Desbloquear conta**.
4. Aplique e confirme.

### Pelo PowerShell

```powershell
# Ver o estado antes
Get-ADUser "joao.silva" -Properties LockedOut, BadLogonCount, LastBadPasswordAttempt |
  Select-Object Name, LockedOut, BadLogonCount, LastBadPasswordAttempt

# Desbloquear
Unlock-ADAccount -Identity "joao.silva"

# Confirmar
Get-ADUser "joao.silva" -Properties LockedOut | Select-Object Name, LockedOut
```

`LastBadPasswordAttempt` é a pista mais útil: diz de que horário vêm as tentativas erradas.

## Como confirmar que resolveu

- `LockedOut` volta para `False`.
- O usuário consegue autenticar.
- **Teste real:** se a conta bloquear de novo em minutos, o desbloqueio não resolveu o problema — só o sintoma.

## Quando escalar

- A conta bloqueia de novo em menos de 30 minutos → há credencial antiga em algum dispositivo (celular com e-mail corporativo, unidade de rede mapeada, script, serviço, outro PC).
- Há tentativas de IP desconhecido → trate como possível incidente de segurança e acione o responsável.
- O bloqueio atinge o domínio inteiro ou vários usuários → política ou controlador de domínio, não usuário.

## Causa mais comum (e a que ninguém lembra)

Celular com a senha antiga configurada no e-mail. O usuário troca a senha no PC, o celular continua tentando a antiga em segundo plano e bloqueia a conta de novo. Antes de culpar o usuário, pergunte: "você tem e-mail configurado no celular ou em outro computador?"

## Testado em

Domínio de laboratório `lab.local` — Windows Server 2022, política de bloqueio em 5 tentativas.

**Última atualização:** 21/10/2026
