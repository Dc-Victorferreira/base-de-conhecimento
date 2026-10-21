# Configurar impressora de rede no Windows 11

## Quando usar

- Impressora nova na rede.
- Usuário trocou de máquina e precisa da impressora que já existe.
- A impressora some da lista depois de atualização do Windows.

## Pré-requisitos

- IP ou nome da impressora (etiqueta no aparelho ou painel de rede).
- O computador na mesma rede/VLAN da impressora.
- A impressora ligada e respondendo: `ping 192.168.0.50`.

Se o `ping` falha, não é problema de driver — pare aqui e verifique cabo, Wi-Fi e VLAN.

## Passo a passo

### Opção 1 — descoberta automática

1. **Configurações** → **Bluetooth e dispositivos** → **Impressoras e scanners**.
2. **Adicionar dispositivo**.
3. Selecione a impressora na lista e siga o assistente.
4. **Imprimir página de teste**.

### Opção 2 — por endereço IP (a que funciona quando a descoberta falha)

1. Abra **Painel de Controle** → **Dispositivos e Impressoras** → **Adicionar uma impressora**.
2. Clique em **A impressora que eu quero não está na lista**.
3. Escolha **Adicionar uma impressora usando um endereço TCP/IP**.
4. Tipo de dispositivo: **TCP/IP**; digite o IP (ex.: `192.168.0.50`).
5. Driver: escolha o modelo correto ou **Windows Update** → fabricante/modelo.
6. **Avançar** → **Concluir** → **Imprimir página de teste**.

### Driver do fabricante (quando o genérico falha)

1. Baixe o driver no site do fabricante, para o modelo exato e Windows 11 64 bits.
2. Instale o pacote antes de adicionar a impressora; muitos já criam a fila.
3. Se o instalador não criar a fila, repita a Opção 2 e escolha o driver recém-instalado.

## Como confirmar que resolveu

- Página de teste impressa.
- Fila vazia em **Impressoras e scanners** → **Abrir fila**.
- Usuário imprime um documento real, do aplicativo que ele usa (não só a página de teste).

## Quando escalar

- `ping` falha e outro computador na mesma rede imprime normalmente → problema de rede/porta, não de estação.
- Erro de driver que volta após reinstalação → modelo sem suporte a Windows 11; validar com o fornecedor.
- Impressora some toda semana → IP dinâmico. Peça IP fixo/reserva DHCP: é a causa mais comum de reincidência.

## Dica de atendimento

Antes de reinstalar driver, reinicie o **spooler**:

```powershell
Restart-Service spooler
```

Elimina a maioria das filas travadas em 10 segundos, sem tocar na impressora.

## Testado em

Windows 11 23H2 com impressora de rede em IP fixo e driver do fabricante.

**Última atualização:** 21/10/2026
