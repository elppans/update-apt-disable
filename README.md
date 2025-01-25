# update-apt-disable

## Script para Desativar Mensagens de Atualização no Ubuntu

- Sistema Ubuntu, mensagem de atualização ao logar via Terminal ou SSH:
  
![image](https://github.com/user-attachments/assets/d8072ea8-ed3a-48ee-8898-7998ede11f59)

Este script automatiza o processo de desativação de mensagens de atualização exibidas no terminal ou ao acessar o sistema via SSH em distribuições baseadas no Ubuntu.

## Funcionalidades

- Desativa mensagens do **MOTD**.
- Impede verificações automáticas de atualização de pacotes.
- Bloqueia notificações sobre novas versões do Ubuntu.
- Desabilita o serviço **unattended-upgrades**.
- Remove o pacote `update-notifier` (opcional).

## Pré-requisitos

- Ubuntu ou sistemas baseados em Debian.
- Permissões de administrador (**root**) para executar o script.

## Como Usar

1. **Clone ou baixe o script** para sua máquina:
   ```bash
   git clone https://github.com/elppans/update-apt-disable.git
   cd update-apt-disable
   ```

2. **Torne o script executável**:
   ```bash
   chmod +x update-apt-disable_ubuntu
   ```

3. **Execute o script com permissões de administrador**:
   ```bash
   sudo ./update-apt-disable_ubuntu
   ```

4. **Reinicie o sistema** para garantir que todas as alterações sejam aplicadas:
   ```bash
   sudo reboot
   ```

## Reversão das Alterações

Caso queira reverter as mudanças feitas pelo script, será necessário:
1. Reativar os arquivos do MOTD:
   ```bash
   sudo chmod +x /etc/update-motd.d/90-updates-available
   sudo chmod +x /etc/update-motd.d/91-release-upgrade
   sudo sed -i 's/^ENABLED=0/ENABLED=1/' /etc/default/motd-news
   ```
2. Reconfigurar os arquivos de atualizações automáticas:
   - Edite manualmente `/etc/apt/apt.conf.d/10periodic` ou restaure o backup (se aplicável).
3. Reativar notificações de versão do Ubuntu:
   ```bash
   sudo sed -i 's/^Prompt=never/Prompt=normal/' /etc/update-manager/release-upgrades
   ```
4. Reativar o serviço `unattended-upgrades`:
   ```bash
   sudo systemctl enable unattended-upgrades
   ```

## Observações

- O script desativa notificações de atualização de forma permanente. Certifique-se de que esta é a funcionalidade desejada.
- Não recomendado para sistemas que precisam de atualizações automáticas para fins de segurança (servidores críticos, por exemplo).

## Licença

Este script é disponibilizado sob a licença [MIT](https://opensource.org/licenses/MIT). Sinta-se à vontade para modificar e distribuir conforme necessário.

---

**Autor:** Elppans Dark Elven  
**Contato:** [mail@email.com](mailto:mail@email.com)

