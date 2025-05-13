# Mudando o nome do switch e o domínio
[Huawei] sysname MEU-SWITCH
[MEU-SWITCH] ip domain-name exemplo.com

# Gerando as chaves RSA (usar pelo menos 2048 bits)
[MEU-SWITCH] rsa local-key-pair create

# Criando o usuário local com senha e permissões
[MEU-SWITCH] aaa
[MEU-SWITCH-aaa] local-user admin password irreversible-cipher MINHA-SENHA-FORTE123
[MEU-SWITCH-aaa] local-user admin privilege level 15
[MEU-SWITCH-aaa] local-user admin service-type ssh
[MEU-SWITCH-aaa] quit

# Configurando as linhas VTY para aceitar SSH
[MEU-SWITCH] user-interface vty 0 4
[MEU-SWITCH-ui-vty0-4] authentication-mode aaa
[MEU-SWITCH-ui-vty0-4] protocol inbound ssh
[MEU-SWITCH-ui-vty0-4] idle-timeout 10 0
[MEU-SWITCH-ui-vty0-4] user privilege level 15
[MEU-SWITCH-ui-vty0-4] quit

# Ativando o servidor SSH
[MEU-SWITCH] stelnet server enable

# Configurando IP na VLAN usada para gerenciamento
[MEU-SWITCH] interface Vlanif10
[MEU-SWITCH-Vlanif10] ip address 192.168.1.2 255.255.255.0
[MEU-SWITCH-Vlanif10] quit

# Salvando as configurações
[MEU-SWITCH] save

################################# Observações #########################################

| Campo                  | O que mudar                                      |
| ---------------------- | ------------------------------------------------ |
| `MEU-SWITCH`           | Nome que você quiser dar ao switch               |
| `exemplo.com`          | Domínio fictício qualquer (obrigatório para SSH) |
| `admin`                | Nome do usuário que você usará para acessar      |
| `MINHA-SENHA-FORTE123` | Sua senha segura                                 |
| `Vlanif10`             | Interface VLAN usada para gerenciamento          |
| `192.168.1.2`          | Endereço IP de gerenciamento do switch           |

