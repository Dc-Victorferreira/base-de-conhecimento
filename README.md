# Base de conhecimento — suporte N1

Cinco procedimentos escritos no formato que uma base de conhecimento corporativa usa: quando usar, pré-requisitos, passo a passo, como confirmar que resolveu e quando escalar.

Escrevi porque no time em que trabalhei não havia base compartilhada e eu repetia a mesma explicação várias vezes por semana. Documentação é parte do trabalho de N1, não um extra.

## Índice

| # | Artigo | Quando usar |
|---|---|---|
| 1 | [Resetar senha no Active Directory](artigos/resetar-senha-active-directory.md) | Usuário esqueceu a senha ou ela expirou |
| 2 | [Desbloquear conta no Active Directory](artigos/desbloquear-conta-active-directory.md) | Conta bloqueada por tentativas de login |
| 3 | [Configurar impressora de rede no Windows 11](artigos/configurar-impressora-rede-windows-11.md) | Impressora nova ou usuário trocou de máquina |
| 4 | [VPN não conecta](artigos/vpn-nao-conecta.md) | Cliente conecta e cai, ou recusa autenticação |
| 5 | [Outlook não sincroniza](artigos/outlook-nao-sincroniza.md) | Caixa parada, envio pendente ou erro de conexão |

## Como escrevo um artigo

```
# Título (verbo + objeto)
## Quando usar
## Pré-requisitos
## Passo a passo
## Como confirmar que resolveu
## Quando escalar
## Testado em / Última atualização
```

Regras que sigo:

- Título começa com verbo: "Resetar", "Desbloquear", "Configurar".
- Passo a passo numerado, com o texto exato que aparece na tela.
- Sempre dizer o que **não** fazer (ex.: não desabilitar conta sem confirmar com o gestor).
- Toda instrução tem um jeito de verificar. Sem verificação, não é procedimento, é palpite.
- Dizer quando parar e escalar — protege o usuário e o técnico.

## Ambiente dos testes

Os procedimentos de Active Directory foram testados em um domínio de laboratório (`lab.local`, Windows Server 2022) com cliente Windows 11. Os demais, em Windows 11 e em cliente VPN/Outlook de teste. Não há dado real de empresa ou usuário aqui.

## Autor

Victor Arthur Ferreira — [LinkedIn](https://linkedin.com/in/victor-arthur-ferreira-064b282a0)
