# Outlook não sincroniza: os 5 primeiros passos

## Quando usar

- Caixa de entrada parada ("Atualizado há 2 horas").
- Mensagens na Caixa de Saída que não saem.
- Erro de conexão com o servidor, ou "tentando conectar".

## Pré-requisitos

- Saber se a conta é Microsoft 365, Exchange local ou IMAP.
- Internet funcionando no computador (teste o navegador antes).

## Passo a passo

1. **Escopo.** É só este usuário? Pergunte ao colega do lado ou olhe o status do serviço da Microsoft. Se for geral, pare o atendimento individual e verifique o serviço.
2. **Modo seguro.** Abra com `Win + R` → `outlook.exe /safe`. Se funcionar no modo seguro, é suplemento (add-in) — desative os suplementos em **Arquivo → Opções → Suplementos** e reative um por um.
3. **Caixa de saída e tamanho do arquivo.** Mais de 50 GB de OST/PST deixa o Outlook lento e travado. Verifique em **Arquivo → Configurações da Conta → Configurações da Conta → aba Arquivos de Dados**.
4. **Recriar o perfil.** **Painel de Controle → Mail → Mostrar Perfis → Adicionar**. Recriar perfil resolveOST corrompido na maioria dos casos, sem perder nada porque a caixa está no servidor (confirme antes que não é conta POP).
5. **Reparo do Office.** **Configurações → Aplicativos → Microsoft 365 → Modificar → Reparo Rápido**; se não resolver, **Reparo Online** (exige internet e fecha o Office).

## Como confirmar que resolveu

- Status muda para "Atualizado agora".
- Enviar um e-mail de teste para o próprio usuário e receber.
- Fechar e abrir o Outlook: mensagens continuam lá.

## Quando escalar

- Vários usuários com o mesmo erro → servidor/serviço, não estação.
- Erro de licença ou "conta desativada" → administração do Microsoft 365.
- Caixa cheia (limite de armazenamento) → decisão de arquivamento é do gestor do usuário, não do suporte.

## Cuidado

- Nunca apague o OST/PST para "testar" antes de confirmar que a conta é Exchange/Microsoft 365. Em conta POP, isso apaga o e-mail.
- Não peça a senha. Se precisar digitar credencial, use o prompt do próprio Outlook com o usuário ao lado.

## Testado em

Outlook para Microsoft 365 no Windows 11, com perfil recriado e reparo rápido.

**Última atualização:** 21/10/2026
