# Rocky Linux 9 - Ansible: DHCP (dhcpd) + DNS (BIND/named)

Este repo instala y configura:

- DNS autoritativo interno con BIND (named), con forwarders opcionales
- DHCP con isc-dhcp-server (dhcpd)
- firewalld (si está disponible) y apertura de puertos
- validaciones de configuración (named-checkconf / named-checkzone / dhcpd -t)

## Requisitos

- Ansible >= 2.15 recomendado
- Target: Rocky Linux 9 (familia RHEL 9)
- Colección: `ansible.posix` (para `ansible.posix.firewalld`)
  - Instalar: `ansible-galaxy collection install ansible.posix`

## Uso rápido

1. Ajusta `inventory/hosts.ini` con la IP/host del servidor Rocky 9.
2. Ajusta variables en `group_vars/all.yml`.
3. Ejecuta:
   ```bash
   ansible-playbook -i inventory/hosts.ini site.yml
   ```
