# Conexiune SSH între două mașini virtuale și Host OS

## Cerință

Să se realizeze o conexiune Telnet sau SSH între două mașini virtuale și host OS-ul în cadrul căruia rulează hipervizorul.

Pentru această temă am ales protocolul **SSH**, deoarece este mai sigur și mai folosit decât Telnet.

---

## Mediu de lucru

- **Host OS:** Windows
- **Hipervizor:** Oracle VirtualBox
- **VM1:** Ubuntu
- **VM2:** Ubuntu
- **Protocol folosit:** SSH
- **Port folosit:** 22

---

## Configurarea rețelei

Pentru fiecare mașină virtuală am folosit două adaptoare de rețea:

1. **Adapter 1: NAT**
   - folosit pentru acces la internet;
   - necesar pentru instalarea pachetelor.

2. **Adapter 2: Host-only Adapter**
   - folosit pentru comunicarea dintre Host OS, VM1 și VM2;
   - permite realizarea conexiunilor SSH în rețeaua locală VirtualBox.

Adresele IP obținute au fost:

```text
Host OS: 192.168.56.1
VM1:     192.168.56.101
VM2:     192.168.56.102
```

---

## Verificarea adreselor IP

Pe fiecare mașină virtuală am folosit comanda:

```bash
hostname -I
```

Rezultate:

```text
VM1: 10.0.2.15 192.168.56.101
VM2: 10.0.2.15 192.168.56.102
```

Adresele importante pentru conexiunea SSH sunt cele din rețeaua Host-only:

```text
VM1: 192.168.56.101
VM2: 192.168.56.102
```

---

## Instalarea serverului SSH

Pe ambele mașini virtuale Ubuntu am instalat OpenSSH Server.

Comenzi folosite:

```bash
sudo apt update
sudo apt install openssh-server -y
```

După instalare, serviciul SSH a fost activat și pornit:

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
```

La verificare, serviciul SSH a fost activ pe ambele mașini virtuale:

```text
Active: active (running)
```

---

## Conexiuni SSH realizate

Au fost realizate următoarele conexiuni:

### 1. Host OS către VM1

Din PowerShell pe Windows:

```bash
ssh ubuntu@192.168.56.101
```

Rezultat: conexiunea către VM1 a fost realizată cu succes.

---

### 2. Host OS către VM2

Din PowerShell pe Windows:

```bash
ssh ubuntu@192.168.56.102
```

Rezultat: conexiunea către VM2 a fost realizată cu succes.

---

### 3. VM1 către VM2

Din terminalul VM1:

```bash
ssh ubuntu@192.168.56.102
```

Rezultat: conexiunea de la VM1 la VM2 a fost realizată cu succes.

---

### 4. VM2 către VM1

Din terminalul VM2:

```bash
ssh ubuntu@192.168.56.101
```

Rezultat: conexiunea de la VM2 la VM1 a fost realizată cu succes.

---

## Dovezi

Capturile de ecran se află în folderul `screenshots`.

Capturile demonstrează:

- adresa IP pentru VM1;
- adresa IP pentru VM2;
- serviciul SSH activ pe VM1;
- serviciul SSH activ pe VM2;
- conexiunea SSH Host OS către VM1;
- conexiunea SSH Host OS către VM2;
- conexiunea SSH VM1 către VM2;
- conexiunea SSH VM2 către VM1.

Structura pentru capturi:

```text
screenshots:
1)vm1_hostname.png
2)vm2_hostname.png
3)vm1_ssh_status.png
4)vm2_ssh_status.png
5)host_to_vm1.png
6)host_to_vm2.png
7)vm1_to_vm2.png
8)vm2_to_vm1.png
```

---

## Concluzie

Am configurat două mașini virtuale Ubuntu în Oracle VirtualBox și am folosit protocolul SSH pentru comunicarea dintre ele și Host OS. Fiecare mașină virtuală a fost configurată cu **NAT** pentru acces la internet și **Host-only Adapter** pentru comunicarea locală.

Serviciul **OpenSSH Server** a fost instalat și pornit pe ambele mașini virtuale, iar conexiunile SSH au fost testate cu succes în ambele direcții:

```text
Host OS -> VM1
Host OS -> VM2
VM1 -> VM2
VM2 -> VM1
```
