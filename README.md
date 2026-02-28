# DHCP + DNS (BIND) en Rocky Linux 9 con Ansible

Repo: https://github.com/carlostrullo/dhcp-dns

Este proyecto configura en **Rocky Linux 9**:

- **DNS** con BIND (`named`)
  - Autoritativo para un dominio interno (`carredondot.local`)
  - Recursión opcional + **forwarders** (por defecto Google: `8.8.8.8`, `8.8.4.4`)
  - Zonas forward y reverse con plantillas Jinja2
  - Validaciones: `named-checkconf`, `named-checkzone`

- **DHCP** con ISC DHCP (`dhcpd`)
  - Subred `192.168.56.0/24`
  - Rango `192.168.56.100-192.168.56.110`
  - Gateway `192.168.56.1`
  - DNS entregado `192.168.56.254`
  - Validación: `dhcpd -t`

- **Firewall (firewalld)**
  - Abre puertos: DNS `53/tcp`, `53/udp` y DHCP `67/udp`

> ⚠️ **Advertencia de seguridad**
>
> DHCP puede afectar a todo un segmento de red. Ejecute este proyecto **solo en una red aislada de laboratorio** (VLAN/host-only/intnet).  
> No lo ejecute en una red productiva sin autorización y sin aislar el segmento.

---

## 1) Prerrequisitos

### 1.1 Control node (donde corres Ansible)

Puedes correr Ansible:

- **En el mismo server** (modo local) ✅ (más simple)
- Desde otra máquina (modo remoto SSH)

Requisitos:

- `git`
- `ansible-core`
- colección `ansible.posix` (para `ansible.posix.firewalld`)

En Rocky / RHEL 9:

```bash
sudo dnf -y install git ansible-core
ansible --version
ansible-galaxy collection install ansible.posix
```
